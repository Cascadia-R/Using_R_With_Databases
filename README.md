# Using R With Relational Databases 
***
### [Aaron Makubuya](https://www.linkedin.com/in/aaronmakubuya/)


***
# Overview

Would you like to learn how R is used to advance valuable information from data stored in relational databases? 
With the proliferation of data and increased reliance on data-driven knowledge, many companies need skilled individuals who can extract meaningful information form data in order to drive informed decisions. 

This intermediate workshop offered at the [2018 Cascadia-R conference](https://cascadiarconf.com/), will introduce you to various methods of using R with databases to derive valuable information from data. The workshop will give you hands-on experience in the following areas:
- how to connect to a database from R. 
- how to create and manage database objects.
- how to issue SQL queries to retrieve and transform your data using R.

***

# Prerequisites

Please be sure to have the following software installed on your machine before the workshop date. If you already have [Virtual box](https://www.virtualbox.org/wiki/Downloads) and/or [Vagrant](https://www.vagrantup.com/) installed on your machine, you do not have to install the software below. Additional material will be provided during the workshop.

### Note:

- Please follow the instructions for your OS and architecture (i.e install 32 bit software for a 32 bit machine and 64 bit software for a 64 bit machine). Needless to say, 64 bit binaries are not compatible with 32 OS and will result in software version incompatability.

#### Windows Users

Install virtual box for windows using the link below:

 - [Virtual box for windows](https://download.virtualbox.org/virtualbox/5.2.12/VirtualBox-5.2.12-122591-Win.exe)

Install vagrant for windows using the link below:

 - [Vagrant for windows](https://releases.hashicorp.com/vagrant/2.1.1/vagrant_2.1.1_x86_64.msi)

***

#### Mac /Linux Users

Install vagrant for mac/linux using the link below:

 - [Vagrant](https://releases.hashicorp.com/vagrant/2.1.1/vagrant_2.1.1_x86_64.dmg)

Install virtual box for mac/linux using the link below:

 - [Virtual box](https://download.virtualbox.org/virtualbox/5.2.12/VirtualBox-5.2.12-122591-OSX.dmg)


# Next steps after installing the software above

### How to use vagrant

#### Step 1

- Open your command prompt and move into vagrant directory containing the 'vagrantfile'.

#### Step 2 

- To start vagrant, type the following command in your command prompt: Vagrant up

#### Step 3

- Open your browser and run R-studio server: type -> localhost:8787

#### Step 4

- user and passord to R-studio server: vagrant

