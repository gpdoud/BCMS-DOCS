[Back to README.md](README.md)

# Azure Architecture of BCMS

BCMS was created and deployed in production mode back in 2018. I used my personal hosting from a company called Winhost which only did Windows systems hosting and, at the time, it only proided *shared* hosting. I did not have server certificate to allow HTTPS support so all traffic was done via HTTP.

I have very little knopwledge of Azure and have never used it because the costs are much higher than my Winhost costs. To effect the transition to Azure, there were a few foundational changes that were required.

1. Azure wants all web traffic to run as HTTPS. HTTPS support was not used previously because I could not use it on Winhost.
2. Azure disallowed accessing JSON files by default. An XML file had to be added to allow reading JSON files which was needed by the Angular code.

## Access to Azure Portal

In order to configure Azure for BCMS, I had to get access to the Azure Portal with significant privileges to create all the objects for the application. I had to contact Chris Ryan (support services for MAX) to get set up with all the privileges I needed. Only then could I access the Azure Portal.

The [Azure Portal](http://portal.azure.com) requires a Microsoft account username and password to start logging in. After they are provided, two factor authentication will send a code to the phone which much be entered into the page. Then, another six digit number must be entered from an authentication app.

All objects created were placed in the BCMS group so they could be easily found.

## SQL Database

The SQL database is under the SQL Server object `bcms-server` and is named `DB_133575_dsibcmsdb` which is the name given when it was deployed to Winhost. It's service tier is `Basic` which has a monthly fee of $4.90 per month with a data limit of 2 GB. 

Once it was defined, the database was easily accessible via SQL Server Management Studion v19.1. The username to access is `bcms-administrator` and the password is the same as the staff password to the MAX video conferencing software. 

I don't know the impact on performance with the Basic service tier selection.

## C# WebAPI

The C# code is using the `DsiBcmsServer` App Service running on Windows with the `Shared D1` shared hosting plan which is privced at `$9.49 per month` plus `$0.013 per hour`. The shared hosting plan may cause the application to seem to freeze for a moment because of other activity on the shared hosting server.

### Migrations

When deploying structural changes to any of the models, a `migration` is required. This process creates a class in the `migrations` folder that will make the required modifications to the SQL tables so they match the class definitions. To create a migration, open the `Package Manager Console` from the View menu. After the class(es) have been changed, the command is:

```
add-migration "added property XYZ to class User"
```

Visual Studion will display the generated migration class in an editor tab. This code should be reviewed to make sure all the required changes were done correctly to the class. When the migration is deemed correct, it can be applied to the database with another command in the `Package Manager Console`:

```
update-database
```

This will apply the new migration to the database updating the schema so that all the tables match the structure of the classes.

### Deploying to Azure

This code is easily deployed to Azure via the `Publish` action in Visual Studio. Just right-click on the solution's project and select `Publish`. Then click the ***Publish*** button and Visual Studio does all the work. The publish process can be viewed in the `Output` window pane.

## Angular 

The Angular code is using the `BcmsNg` App Service running on Windows with the `Free F1` hosting plan which is free but is limited to 60 minutes of ACU/vCPU (whatever that means?). When the Angular code is started in a browser, the files in Azure are downloaded to the user's browser. From then on, the browser code is communicating with the C# code directly so I think there should be very little time spent on this App Service.

### Deploying

To deploy the Angular application, a production build must be done. This turns all the many source files into one HTML file, three Javascript files and one CSS file. There is an `assets` folder which is deployed with all its contents include the important `config.json` configuration file. To build the production code, I execute this Angular command:

```
ng build --configuration production --base-href="./"
```

This command places the production code in the `dist` folder of the project.

To place the code into Azure, select the `BcmsNg` web app. Scroll down the left pane to `Development Tools` and click `Advanced Tools`. When Advanced Tools displays, click `Go`. This will start a new tab displaying the `Kudu`. Click on the `Debug Console` at the top and click `CMD` or `PowerShell`. This will display a list of files and folders at the top and a console display at the bottom. Click on `site` then `wwwroot` go see the project root folder where Angular code should be deployed.

At a minimum, the HTML, all the .JS files, and the .CSS file must be deployed together. Select them from the `dist` folder then drag and drop them in the files and folders window. If any of the previous files are still there, they should be deleted. You can view the `modified` column to tell if it is an old file that was not replaced. Delete it by clicking the circle icon on the left.

That's it.

## Get External IP

Because all web sites are using HTTPS, there is a small web site that is used by BCMS to get the external IP address of the user. That code was redeployed to Azure in the `bcmsGetIp` web app. This app is also using the `Free F1` App Service (see Angular above for details). This app does not required any maintenance as it provides only the one, simple function.