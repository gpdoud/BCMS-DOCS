# Architecture of BCMS

BCMS is composed of two private repository projects in the gpdoud Github:

* DsiBcmsServer - C#, Entity Framework Core, WebAPI
* DsiBcmsClient - Angular

## DsiBcmsServer

This is a Visual Studio project using C#, Entity Framework Core, and WebAPI. It was created using the Entity Framework Core "Code First" process which can be used when creating an application that includes a SQL Server database. 

The code is tied to the SQL database by a connection string that is defined in the `appsettings.json` file. The specific connection string selected is defined in the `Program.cs`.

The developer codes the "models" which are the classes representing the SQL tables. Additional information must be added to the class to provide all the information needed to create the SQL tables. For example, when a class property is a string type, SQL will need the maximum length of the string. This additional information can be provided either by "attributes" or by "Fluid-api". BCMS uses both.

Once the models are created, executing an Entity Framework Core script will read the model and generate a class called a "Migration" that contains code to create or modify the SQL Server database. Creating this migration does NOT make any changes to SQL. Once the migration has been created, it should be reviewed by the developer to make sure it accurately defines the changes to the database. If there is an error, the migration can be removed, the class fixed, and the migration created again.

Once the migration is verified, another Entity Framework script will execute the migration code which will update the SQL database.

With "Code first", the class and the table are always in sync. No SQL syntax is required.

### Deploying DsiBcmsServer

To deploy the project to a remote server, Visual Studio provides a process called "Publish" for the project.

Publishing to a non-Azure hosting environment requires configuration such as authentication, the location of the server, the folder to place the code, and a few other pieces of information. Once created, to publish subsequent code changes required simply pressing the "Publish" button. It is very simple.

When a new code version requires changes to the SQL tables, these updates should be done first and can be done from Visual Studio before the code is published.

There is an Entity Framework Core script command `update-database` that will review the migrations in the project and apply those not already applied to the hosted SQL database. Once this is done, the code can be published to the hosted server.

## DsiBcmsClient

This project is an Angular SPA (Single Page Application) project. Though it is architected in the same realm as the capstone project taught in the coding boot camps.

Configuration is defined by a `config.json` file stored in the `src/assets` folder. The file has just a few configuration options:

- *logServerity*: defines the log messages that will be displayed in the browser console.
- *checkIp*: If set `true` will check that the user's IP addres exists in the `validIps` table.
- *checkLogin*: if set to `true` will require every component to check that a user is logged in.
- *baseUrl*: this is the base URL to the C# application
- *validIps*: this is an array of objects with this format: `{ name: xxx, ip: 0.0.0.0 }`. The name value can be anything as it is just a description of the user's IP. The ip is the external IP address of a user.

### Deploying DsiBcmsClient

To deploy the project, the production version of the code must be created before deployment. This is the current script and parameters to ready the code for deployment:

`ng build --configuration production --base-href="./"`

After this is executed successfully, there will be a new folder called `dist` in the project. It contains all that needs to be deployed by just copying all the files and folders. The first time it is deployed, it is likely that the `baseUrl` must be modified to point to the base url of the C# service.