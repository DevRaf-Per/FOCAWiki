FOCA needs a SQL database to run. In this tutorial we will learn how to set up a SQL Server Express instance, step by step.

## Database installation

First, get the latest version of SQL Server Express from the Microsoft official [website](https://www.microsoft.com/es-es/sql-server/sql-server-downloads) (don't worry, it's completely free!).

Once downloaded, select "Basic installation" and follow the installation wizard, sticking to the defaults (unless you know exactly what you are doing).

![foca_bdinstall](https://user-images.githubusercontent.com/16854757/74440892-20fcdb80-4e6f-11ea-977c-9ed6b9818787.png)

Hopefully, you will end up with a fully working SQL Express instance.

## FOCA configuration

When you run FOCA for the first time you will be prompted with a warning...

![foca1](https://user-images.githubusercontent.com/16854757/74443170-09bfed00-4e73-11ea-99c4-bf7f061e138e.PNG)

... followed by a window to set up a database connection:

![foca2](https://user-images.githubusercontent.com/16854757/74443168-09275680-4e73-11ea-9168-b3664b608fad.png)

First, enter the server name in the textbox. Unless you have manually changed the instance name during the installation, it should be `.\SQLEXPRESS`.

Then, choose your preferred authentication method. Here you have two options:
* Use **Windows Authentication** (integrated authentication). This is the default option, which should work in most cases. It makes use of the Windows user account, so no additional credentials are required.
* Use the **SQL Server Authentication**. To do so, you will need to create a login in your SQL server instance (see below), and then enter the credentials in the corresponding text boxes.

![foca3](https://user-images.githubusercontent.com/16854757/74443169-09275680-4e73-11ea-9639-49538231e87e.PNG)

You can now test the connection by clicking the "Test" button. If everything is fine, you will see a "Success!" message. Finally, click on "Connect". FOCA should now work. 

### Creating a custom SQL login

In case you want to use SQL authentication in FOCA, follow these steps:

1. First, you must enable the 'mixed' authentication mode in your SQL instance. To do so, press `Windows+R` and type 'regedit'. You should see something like the panel in the figure. Then, navigate to the registry key of your SQL Server instance, something like `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.SQLEXPRESS\MSSQLServer`. Finally, in the right panel, set the 'LoginMode' to 2 (which means 'Mixed mode') and restart your SQL Server instance.

![foca_regedit](https://user-images.githubusercontent.com/16854757/74442312-91a4f780-4e71-11ea-9901-690e2aa68264.PNG)

1. Open a terminal and type

`sqlcmd -S .\SQLEXPRESS`

This will open a sqlcmd interface with your instance (remember, if you changed the instance name, modify the command accordingly).

2. Then, create a login and a user for the Foca database

```
USE Foca
GO
CREATE LOGIN #USERNAME# WITH PASSWORD='#PASSWORD'
GO
CREATE USER #USERNAME# FOR LOGIN #USERNAME#
GO
```

3. And finally, grant read/write permissions to the new user

```
EXEC sp_addrolemember 'db_ddladmin', '#USERNAME#'
GO
EXEC sp_addrolemember 'db_datareader', '#USERNAME#'
GO 
EXEC sp_addrolemember 'db_datawriter', '#USERNAME#'
GO
```

