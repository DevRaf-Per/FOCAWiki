FOCA needs a SQL database to run. In this tutorial we will learn how to set up a SQL Server Express instance, step by step.

## Database installation

First, get the latest version of SQL Server Express from the Microsoft official [website](https://www.microsoft.com/es-es/sql-server/sql-server-downloads) (don't worry, it's completely free!).

Once downloaded, select "Basic installation" and follow the installation wizard, sticking to the defaults (unless you know exactly what you are doing).

![install2](https://user-images.githubusercontent.com/16854757/74513899-e1d09800-4f0b-11ea-9df5-2096556f5ca5.png)

Hopefully, you will end up with a fully working SQL Express instance.

## FOCA configuration

When you run FOCA for the first time you will be prompted with a warning...

![foca1](https://user-images.githubusercontent.com/16854757/74443170-09bfed00-4e73-11ea-99c4-bf7f061e138e.PNG)

... followed by a window to set up a database connection.

First, enter the server name in the textbox. Unless you have manually changed the instance name during the installation, it should be `.\SQLEXPRESS`.

Then, choose your preferred authentication method. Here you have two options:
* Use **Windows Authentication** (integrated authentication). This is the default option, which should work in most cases. It makes use of the Windows user account, so no additional credentials are required.
* Use the **SQL Server Authentication**. To do so, you will need to create a login in your SQL server instance (see below), and then enter the credentials in the corresponding text boxes.

![foca_integrated](https://user-images.githubusercontent.com/16854757/74517204-fe6fce80-4f11-11ea-85f5-9ef5219eda07.png)

Finally, click on "Connect". FOCA should now work. 

### Creating a custom SQL login

In case you want to use SQL authentication in FOCA, follow the steps described in the official tutorials: [create a database user](https://docs.microsoft.com/en-gb/sql/relational-databases/security/authentication-access/create-a-database-user?view=sql-server-ver15) and [create a database role](https://docs.microsoft.com/en-gb/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql?view=sql-server-ver15).

