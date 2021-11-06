# QuickDBS.API

A tiny library to generate models, controllers and there upon generate all the Web APIs from a supported QuickDBS database service. It imports all the Models from the table names of the selected database and generate controllers there upon.

## Required Libraries
You need to use one of the supported QuickDBS database packages in order to generate Web APIs.  Currently, you can generate for SQLite, SQL Server and MySql databases for which the packages are already available on the NuGet.

## Usage
- Create an empty **ASP.NET Core Web API** project.
- Add dependency from NuGet to either **QuickDBS.SQLite**, **QuickDBS.SQLServer** or **QuickDBS.MySQL**.
- Add `using QuickDBS;` to the **Startup.cs** file. 
- In the **Startup.cs** class, add the following in the **ConfigureServices** method

        var dbServer = new SQLServer("databasename");  // Use SQLite or MySQL if that's what you want
        services.AddSingleton(dbServer);
        APIs.Create(dbServer);

- Run the project once so that the Models, Controllers and the Web APIs are generated.
- Remove or comment the `APIs.Create(dbServer);` line so that it doesn't keep on repeating the generation process.
- That's it. Now, you should have all the models in the Models folder and controllers in the Controllers folder. Run the project and start using the Web APIs.
