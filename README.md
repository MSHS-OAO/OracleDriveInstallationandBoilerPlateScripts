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
- Intstalling the unixodbc
- Downloading the necessary zip files from Oracle site
- Extracting zip files to `/opt/oracle` directory
- Populating the `/opt/oracle/instantclient_21_5/network/admin/` folder
- Creating and Populating the odbc.ini and odbcinst.ini
- Exporting to the path
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

## Intstalling the unixodbc
In order to facilitate the ODBC connections we need `unixodbc`. You can install unixodbc using the following command `apt-get install unixodbc`

## Downloading the necessary zip files from Oracle site

As of now, You should still be in your home directory. You can confirm this typing the commans `pwd`. If you aren't in the home directory you can navigate to home directory using the following command `cd /home/<username>/` replace <username> with your user name that you used for logging into the server.

Now, Before downloading the instant client zip folders to your home directory, Check the version of OS and architecture of the server using the following commands.
- For checking the OS version use `lsb_release -a`
- For checking the server architecture use `uname -m`

![OS Output](/assets/OS.PNG)

Based on the above output, Download the zip files from following [link](https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html)

We need the following packages from the link mentioned above:
    
| Package                  | Description                                                                                           |
|:------------------------:|:-----------------------------------------------------------------------------------------------------:|
| Basic Package (ZIP)      | All files required to run OCI, OCCI, and JDBC-OCI applications                                        |
| SQL*Plus Package (ZIP)   | The SQL*Plus command line tool for SQL and PL/SQL queries                                             |
| SDK Package (ZIP)        | Additional header files and an example makefile for developing Oracle applications with Instant Client|   
| ODBC Package (ZIP)       | Additional libraries for enabling ODBC applications                                                   | 
    
We can download the above mentioned zip files using the following commands:
    
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
- Navigate to `/opt/oracle` folder using the following command `cd /opt/oracle`
- Now, Extract all the four zip files you downlaoded using the following set of commands
```
unzip /home/<username>/instantclient-odbc-linux.x64-21.5.0.0.0dbru.zip 
unzip /home/<username>/instantclient-basic-linux.x64-21.5.0.0.0dbru.zip 
unzip /home/<username>/instantclient-sdk-linux.x64-21.5.0.0.0dbru.zip 
unzip /home/<username>/instantclient-sqlplus-linux.x64-21.5.0.0.0dbru.zip 
```
Note:
- Replace <username> with your "username"
- The unzip command extracts the files into folder with name `instantclient_21_5` withib `/opt/oracle`. Depending on which version you installed, The name of folder `instantclient_21_5` might be different for you so do not panic!
    
## Populating the opt/oracle/instantclient_21_5/network/admin/

Once all the four files are unzipped you have to copy the contents of cloud wallet to `/opt/oracle/instantclient_21_5/network/admin/`. At the time when credentials are first mailed to you, You would have been provided with instructions to find the zipfile in the shared drive. If you have trouble finding the cloud wallet zip file contact ***Data Warehouse Working Group***. We are not posting here for security reasons.
    
Now, Navigate to /network/admin folder using the follwoing command `cd /opt/oracle/instantclient_21_5/network/admin/` and copy the contents of cloud wallet to this folder.

If the `/network/admin/` folder doesn't exist, Create one using the following command `mkdir /opt/oracle/instantclient_21_5/network/admin/`!

## Creating and Populating the odbc.ini and odbcinst.ini

## Exporting to the path
> This is the critical step of the process, Make sure to do this!

In order to export the path, Follow the below instructions:
- Open the `.bachrc` file using the command `nano ~/.bashrc`
- Paste the following lines at the end of the file:

    ```
    ORACLE_HOME=/opt/oracle/instantclient_21_5/
    PATH=$ORACLE_HOME:$PATH
    LD_LIBRARY_PATH=$ORACLE_HOME
    export ORACLE_HOME
    export LD_LIBRARY_PATH
    export PATH
    ```
## Checking the installation
    
## Possible errors and solutions (Not extensive!!)
   


