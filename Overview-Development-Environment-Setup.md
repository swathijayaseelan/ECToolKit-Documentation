#Overview Development Environment Setup#

Overview application is developed on Ruby on Rails (ROR) platform. Hence Windows is not the natural development environment, as Windows does not have some of the native libraries that are required for ROR development. However we can use CYGWIN to get the the application working on an Windows environment. The below documentation describes the steps to install CYGWIN, Ruby, Ruby Version Manager, Rails and Postgresql which are need to for the setup of Overview in Windows environment. 

##Software Needed##

1. CYGWIN - latest version
2. Ruby - 2.1.2
3. Rails - 4.2.1
4. Postgresql - latest version.

##Installing CYGWIN##
Cygwin is a large collection of GNU and Open source tools which provide functionality similar to Linux distros on Windows.

1. Download Cygwin from https://www.cygwin.com/setup-x86.exe (32 bit) and https://www.cygwin.com/setup-x86_64.exe (64 bit). This will download the installer. Select the default installation parameters.
2. Ensure that the below listed packages are also included in the list. (Use search text box at the top to get these packages).
	* Net
		* curl
		* libcurl-devel
	*Database
		* postgresql
	* Devel
		* make
		* gcc-core
		* gcc-g++
		* git:Distributed Version Control System
	* Ruby (Entire package)
	* Libs
		* libiconv
		* libiconv2
		* libiconv-devel
		* libxml2
		* libxml2-devel
		* libxslt
		* libxslt-devel
		
3. Once this is installed, the Cygwin is ready for use

##Installing Ruby Version Manager##
1. Run the command to import the keys for RVM
```command curl -sSL https://rvm.io/mpapis.asc | gpg --import -```
2. Run the below command to install RVM
```curl -L https://get.rvm.io | bash -s stable```

##Postgresql Installation##
1. Download postgresql from http://www.enterprisedb.com/products-services-training/pgdownload and follow the default installation steps. Install pgadmin III as well for easy use.
2. Connect to your database server using the psql command. In case psql command is not found add /usr/sbin to the PATH using the command 
```
export PATH=/usr/sbin:$PATH
psql -h localhost -U <username>
postgres=# create database syllabus_lti_development;
```

##Get Overview Application Set up##
* Clone the Overview repository using the below command under your workspace
```git clone https://github.com/HBSAWS/Overview.git```
* Run the below command to set the curb get to use system libraries.
```bundle config curb --use-system-libraries```
* Run the below command to download all the gems needed for the application.
```bundle install```
if you encounter any error, run ```bundle update``` and then try doing ```bundle install``` again.
* Edit the database.yml file and under the configuration for development add below. (Please don't commit this change)
```
 adapter: postgresql
  encoding: unicode
  database: syllabus_lti_development
  host: localhost
  username: postgres
  password: *******
  pool: 5
  timeout: 5000
  port: 5432
```
* Copy the below files under config and rename them as below
Original Name | New Name
------------- | ---------
email.yml.example | email.yml
redis.yml.example | redis.yml
s3\_config\_.yml.example | s3\_config.yml
* Run the below command to create the tables for the application
```bundle exec rake db:migrate```
* Start the application by running the command
```rails server```




