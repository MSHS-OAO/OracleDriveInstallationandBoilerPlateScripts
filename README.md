# Steps to Install Oracle Drivers on Servers with Linux OS

# Description

This README should serve as documentation for installing the Oracle drivers on servers running using Linux OS, Specifically Ubuntu distribution. 
If you feel that the instructions aren't correct or found a better way to install drivers or instructions aren't intuitive, please contact ***Data Warehouse Working Group*** to discuss.

> Folder structure

```
    .
    ├── assets                  # Contains all the images used in markdown file
    ├── boilerplate.R           # Code for connecting to database while using workbench
    ├── boilerplate.Rmd         # Code for connecting to database while using RConnect
    └── README.md               # Documentation
```

# Table of Contents

- Java Installation
- Downloading the necessary zip files from Oracle site
- Extracting zip files to `/opt/oracle` directory
- Populating the `/opt/oracle/instantclient_21_5/network/admin/` folder
- Creating and Populating the odbc.ini and odbcinst.ini
- Exporting to the path
- Intstalling the unixodbc
- Checking the installation
- Possible errors and solutions (Not extensive!!)

### Note
> Before proceeding into following steps, make sure you have root access on the system. If you don't, contact the system administrator(s) in order to get the root access.

## Java Installation
You can install Java on a machine running with Ubuntu following the steps:
- Login as root user using command `sudo su` . This will trigger you to type the password and put the same passowrd you used to login to the server.
- Update the packages using the following command `apt-get update`
- Check for the latest LTS version of Java using the following [link](https://www.oracle.com/java/technologies/downloads/)
- For example, At the time of authoring this documentation, The latest LTS version of java is 17

![Java LTS](/assets/JAVALTS.PNG)
- Since 17 is latest LTS version, We'll use the following commands install `apt-get install openjdk-17-jdk ` and `apt-get install openjdk-17-jre`
- If the installation is successful, We can check the installtion using following command `java --version`. The output should be something similar to this:

![Java Output](/assets/JAVAVERSION.PNG)


## Downloading the necessary zip files from Oracle site

As of now, You should still be in your home directory. You can confirm this typing the commans `pwd`. If you aren't in the home directory you can navigate to home directory using the following command `cd /home/<username>/` replace <username> with your user name that you used for logging into the server.

Now, Before downloading the instant client zip folders to your home directory, Check the version of OS and architecture of the server using the following commands.
- For checking the OS version use `lsb_release -a`
- For checking the server architecture use `uname -m`

![OS Output](/assets/OS.PNG)

Based on the above output, Download the zip files from following [link](https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html) 
    
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
    
```
wget https://download.oracle.com/otn_software/linux/instantclient/215000/instantclient-basic-linux.x64-21.5.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/215000/instantclient-sqlplus-linux.x64-21.5.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/215000/instantclient-sdk-linux.x64-21.5.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/215000/instantclient-odbc-linux.x64-21.5.0.0.0dbru.zip
```
#### Note:
- We can get the above links by copying the link against name of the package.
- Zipfiles are downloaded into your home directory. Now create a folder to unzip the files to `/opt/oracle/` using the following command `mkdir /opt/oracle`

## Extracting zip files to '/opt/oracle' directory

## Populating the opt/oracle/instantclient_21_5/network/admin/

## Creating and Populating the odbc.ini and odbcinst.ini

## Exporting to the path

## Intstalling the unixodbc

## Checking the installation
    
## Possible errors and solutions (Not extensive!!)
   


