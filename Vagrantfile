# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.box_version = "201803.24.0"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest:8787, host:8787 # Rstudio port
  config.vm.network "forwarded_port", guest:5432, host:5432 # 

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y postgresql git ruby r-base gdebi-core libcurl4-openssl-dev libxml2-dev postgresql-server-dev-all
    mkdir Workspace
    cd Workspace
    git clone https://github.com/lorint/AdventureWorks-for-Postgres.git
    git clone https://github.com/Cascadia-R/Using_R_With_Databases.git
    cd AdventureWorks-for-Postgres/
    wget https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip
    unzip AdventureWorks-oltp-install-script.zip
    sudo apt-get install openjdk-8-jdk
    wget https://jdbc.postgresql.org/download/postgresql-42.2.2.jar
    sudo R CMD javareconf
    sudo rstudio-server restart
    ruby update_csvs.rb
    sudo -u postgres psql -c "CREATE USER vagrant WITH PASSWORD 'jw8s0F4';";
    sudo -u postgres psql -c "CREATE DATABASE adventureworks OWNER vagrant;"
    sudo -u postgres psql -c "ALTER ROLE vagrant SUPERUSER;"
    sudo -u vagrant psql -d adventureworks < install.sql
    sudo -u postgres psql -c "ALTER ROLE vagrant NOSUPERUSER;"
    sudo echo "host    adventureworks             vagrant  all                     md5" >> /etc/postgresql/10/main/pg_hba.conf
    sudo sed -i "s/#listen_addresses = 'localhost'/listen_addresses = '0.0.0.0'/" /etc/postgresql/10/main/postgresql.conf
    sudo service postgresql restart
    wget https://download2.rstudio.org/rstudio-server-1.1.442-amd64.deb
    gdebi -n rstudio-server-1.1.442-amd64.deb
    sudo -u vagrant mkdir -p '/home/vagrant/R/x86_64-pc-linux-gnu-library/3.4'
    sudo -u vagrant /usr/bin/Rscript -e "install.packages(c('tidyverse', 'dygraphs', 'DT', 'glue', 'RPostgreSQL'), lib = '/home/vagrant/R/x86_64-pc-linux-gnu-library/3.4', quiet = TRUE)"
    sudo rstudio-server restart
  SHELL
end
