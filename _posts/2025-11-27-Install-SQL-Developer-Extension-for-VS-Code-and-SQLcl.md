## Connect to Oracle Database with VS Code using SQL Developer Extension and SQLcl

  ![Apex](/docs/assets/images/sqlcl-1.png)
                      

### Introduction:
In this blog post I will show you how to install Oracle SQL Developer Extension for VS Code and SQLcl. SQLcl is included with the Oracle SQL Developer Extension for VS Code.
The extension provides integrated command-line functionality through SQLcl, allowing users to spawn CLI sessions to their database directly within VS Code.

### Pre-Requisite:
Installed VS code (Visual Studio Code) 
Access to Oracle Database from cloud or on-prem

### Steps:

From within VS Code, navigate to **Extensions**, search for Oracle and **"Oracle SQL Developer Extension for VSCode"** will appear on the top of the results. Click Install

 ![Apex](/docs/assets/images/sqlcl-2.png)  
 
![Apex](/docs/assets/images/sqlcl-3.png)

Once installed, navigate to SQL Developer Extension for VS Code located in activity Bar.

![Apex](/docs/assets/images/sqlcl-5.png)

Click on the plus(+) sign to create database connection.

![Apex](/docs/assets/images/sqlcl-5-1.png)

Enter your Oracle database connection details and test it and save it.

![Apex](/docs/assets/images/sqlcl-6.png)

Your new connection will appear in the Primary Side Bar. Click the connection name. In my case it's test1.
   Click the connection name establishes a connection to the target database and reveals various database objects.

![Apex](/docs/assets/images/sqlcl-7.png)

Right click on the connection name and you can see it installed SQL Worksheet, SQL Notebook and SQLcl.

![Apex](/docs/assets/images/sqlcl-8.png)

In my next blog post, I will show you how to use these tools to run queries.
   




   

   
