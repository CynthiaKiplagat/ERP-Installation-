# ERP-Installation
My experience in installing and managing ERPNext (v14) on a production and development environment.
Ubuntu 22.04
# Prerequisites
-Node.js version 16 and 18

-Python 3.10+

# Installation Process
### Update & upgrade server packages
-sudo apt-get update -y

-sudo apt-get upgrade -y

### Create a new sudo user 
-sudo adduser erpuser

-usermod -aG sudo erpuser

### Switch to the new user
-su erpuser

### Installation GIT

-sudo apt-get install git

### Install python and its enviroment

-sudo apt-get install python3-dev python3.10-dev python3-setuptools python3-pip python3-distutils

-sudo apt-get install python3.10-venv

### For repository management install software properties

-sudo apt-get install software-properties-common

### Install Mariadb

-sudo apt install mariadb-server mariadb-client

### Install Redis Server

-sudo apt-get install redis-server

### Install other necessary packages (for fonts, PDFs, etc)

-sudo apt-get install xvfb libfontconfig wkhtmltopdf

-sudo apt-get install libmysqlclient-dev

### Configure mysql server

-sudo mysql_secure_installation

### Edit the MySQL default config file

-sudo nano /etc/mysql/my.cnf

-add the following 

> [mysqld]
  > 
  > character-set-client-handshake = FALSE
  > 
  > character-set-server = utf8mb4
  > 
  > collation-server = utf8mb4_unicode_ci
> [mysql]
  > 
  > default-character-set = utf8mb4

#### Restart the MySQL server (for the config to take effect)

-sudo service mysql restart

### Install Curl,NPM and Yarn

-sudo apt install curl

-curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash

-source ~/.profile

-nvm install 16.15.0

-sudo npm install -g yarn

### Install Frappe-Bench

-sudo pip3 install frappe-bench

#### Initialise Frappe-Bench

-bench init --frappe-branch version-14 frappe-bench

##### Go to Frappe Bench directory

-cd frappe-bench/

#### Change user directory permissions

-chmod -R o+rx /home/erpuser/

#### Create a New Site

-bench new-site firsttime

### Install ERPNEXT AND OTHER APPS

-bench get-app payments

-bench get-app --branch version-14 erpnext

-bench get-app hrms

### Install all the Apps

-bench --site firsttime install-app erpnext

-bench --site firsttime install-app hrms

### ERPNEXT  in Development

-bench start

-bench --site firsttime enable-scheduler

-bench --site firsttime set-maintenance-mode off

### ERPNEXT in Production

#### set the production environment

-sudo bench setup production frappe

-bench setup nginx

-sudo supervisorctl restart all

-sudo bench setup production frappe












