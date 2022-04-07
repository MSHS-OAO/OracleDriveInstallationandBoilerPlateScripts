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
- 

### Note
> Before proceeding into following steps, make sure you have root access on the system. If you don't, contact the system administrator(s) in order to get the root access.

## Java Installation
You can install Java on a machine running with Ubuntu following the steps:
- Login as root user using command `sudo su` . This will trigger you to type the password and put the same passowrd you used to login to the server.
- Update the packages using following command `apt-get update`
- Check for the latest LTS version of Java using the following [link](https://www.oracle.com/java/technologies/downloads/)
- For example, At the time of authoring this documentation, The latest LTS version of java is 17
![Java LTS](/assets/JAVALTS.PNG)
- Since 17 is latest LTS version, We'll use the following commands install `apt-get install openjdk-17-jdk ` and `apt-get install openjdk-17-jre`
- If the installation is successful, We can check the installtion using following command `java --version`. The output should be something similar to this:
![Java Output](/assets/JAVAVERSION.PNG)


## Downloading the necessary zip files from Oracle site

Provide instructions and examples for use. Include screenshots as needed.

To add a screenshot, create an `assets/images` folder in your repository and upload your screenshot to it. Then, using the relative filepath, add it to your README using the following syntax:

    ```md
    ![alt text](assets/images/screenshot.png)
    ```
## Extracting zip files to '/opt/oracle' directory

## Populating the opt/oracle/instantclient_21_5/network/admin/

## Creating and Populating the odbc.ini and odbcinst.ini

## Exporting to the path

## Intstalling the unixodbc

## Checking the installation
    
## Possible errors and solutions (Not extensive!!)
   


