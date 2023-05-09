# Steps to Install Oracle Drivers on Servers with Linux OS

# Description

This README should serve as documentation for installing the Oracle drivers on servers running using Linux OS, Specifically Ubuntu distribution. 
If you feel that the instructions aren't correct or found a better way to install drivers or instructions aren't intuitive, please contact ***Data Warehouse Work Group*** to discuss.

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
> Before proceeding into following steps, make sure you have root access on the system. If you don't, contact the ***Data Warehouse Work Group*** in order to get the root access.

## Java Installation
You can install Java on a machine running with Ubuntu following the steps:
- Login as root user using command `sudo su` . This will trigger you to type the password and put the same passowrd you used to login to the server.
- Update the packages using the following command `apt-get update` amd `apt-get upgrade`
- Check for the latest LTS version of Java using the following [link](https://www.oracle.com/java/technologies/downloads/)
- For example, At the time of authoring this documentation, The latest LTS version of java is 17

![Java LTS](/assets/JAVALTS.PNG)
- Since 17 is latest LTS version, We'll use the following commands install `sudo apt install openjdk-17-jdk `
- If the installation is successful, We can check the installtion using following command `java --version`. The output should be something similar to this:

![Java Output](/assets/JAVAVERSION.PNG)

## Intstalling the unixodbc
In order to facilitate the ODBC connections we need `unixodbc`. You can install unixodbc using the following command `apt-get install unixodbc`

## Downloading the necessary zip files from Oracle site

As of now, You should still be in your home directory. You can confirm this typing the command `pwd`. If you aren't in the home directory you can navigate to home directory using the following command `cd /home/<username>/` replace <username> with your user name that you used for logging into the server.

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
- Zipfiles are downloaded into your home directory. Now create a folder using the following command `mkdir /opt/oracle` to unzip the files.

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
- The unzip command extracts the files into folder with name `instantclient_21_5` within `/opt/oracle`. Depending on which version you installed, The name of folder `instantclient_21_5` might be different for you so do not panic!
    
## Populating the opt/oracle/instantclient_21_5/network/admin/

Once all the four files are unzipped you have to copy the contents of cloud wallet to `/opt/oracle/instantclient_21_5/network/admin/`. At the time when credentials are first mailed to you, You would have been provided with instructions to find the zipfile in the shared drive. If you have trouble finding the cloud wallet zip file contact ***Data Warehouse Working Group***. We are not posting here for security reasons.
    
Now, Navigate to /network/admin folder using the follwoing command `cd /opt/oracle/instantclient_21_5/network/admin/` and copy the contents of cloud wallet to this folder.

If the `/network/admin/` folder doesn't exist, Create one using the following command `mkdir /opt/oracle/instantclient_21_5/network/admin/`!

## Creating and Populating the odbc.ini and odbcinst.ini

Create/Modify the `odbcinst.ini` file using the following command `nano /etc/odbcinst.ini`. Then add the following lines to end of the file:

```    
[Oracle 21_5 ODBC driver]
Description     = Oracle ODBC driver for Oracle 21_5
Driver          = /opt/oracle/instantclient_21_5/libsqora.so.21.1
Setup           =
FileUsage       =
CPTimeout       =
CPReuse         =
```
Note: 
- The line [Oracle 21_5 ODBC driver] should be modified based on the exisiting drivers that are setup in your server
- The third line in above lines code should be modified according the path and version of instant client downloaded

Create/Modify the `odbc.ini` file using the following command `nano /etc/odbc.ini`. Then add the following lines to end of the file:

```
[OAO Cloud DB <yourname>]
Application Attributes = T
Attributes = W
BatchAutocommitMode = IfAllSuccessful
BindAsFLOAT = F
CloseCursor = F
DisableDPM = F
DisableMTS = T
Driver = Oracle 21_5 ODBC driver
DSN = OracleODBC-12c
EXECSchemaOpt =
EXECSyntax = T
Failover = T
FailoverDelay = 10
FailoverRetryCount = 10
FetchBufferSize = 64000
ForceWCHAR = F
Lobs = T
UserID = <username>
Password = <password>
ServerName = <from tnsnames.ora>
```
Note: 
- The line [OracleODBC-21_5] should be modified based on the exisiting drivers that are setup in your server
- The driver name `Driver = Oracle 21_5 ODBC driver` should match as per what's specified in the `odbcinst.ini` file

## Exporting to the path
> This is the critical step of the process!!

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
 - To save the file hit `CTRL+O`, Press Y
 - Then `CTRL+X` to exit
 - Lastly, `export TNS_ADMIN=/opt/oracle/instantclient_21_5/network/admin/`
    
## Checking the installation
> Checking if all the dependencies are correctly mapped. Use the following command `ldd /opt/oracle/instantclient_21_5/libsqora.so.21.1`. If the path is coorectly setup, Then the output should be similar to as shown below:

![LDD Output](/assets/LDD.PNG)
    
Note that in the image, All the paths are showing up. If the paths aren't correctly mapped in the previous step, You'll find string like `Not Found` against the file name on RHS of image shown above.

> Checking the connection using sqlplus package:
Use the following command to test the connection to OAO Database, `sqlplus '<username>/<database password provided to you>@<connection string specified in tsnames.ora file in zip file provided to you.>'`

Note: Just copy the sring after first equal to symbol in tsnames.ora file

If the connection is successfully established, The output should be as shown below:
    
![SQLPLUS Output](/assets/SQLPLUS.PNG)

To exit from the connection, Just type `exit()`
    
> Checking the connection using unixodbc package:
Use the following command to test the connection to OAO Database, `isql "OracleODBC-21_5" "<username>" "<database password provided to you>" -v`

If the connection is successfully established, The output should be as shown below:
    
![SQLPLUS Output](/assets/ISQL.PNG)

To exit from the connection, Just type `quit`

## Possible errors and solutions (Not extensive!!)
   


