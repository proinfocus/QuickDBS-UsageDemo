# QuickDBS.API
A tiny library to generate Models and APIs from a supported QuickDBS database service. It imports all the Models from the table names of the selected database and generate Minimal APIs/Controllers there upon.
<br/>
<br/>
## What's New
Now this library supports generating Minimal APIs using `CreateMinimalAPIs` method.
<br/>
<br/>
## Required Libraries
You need to use one of the supported QuickDBS database packages in order to generate APIs.  Currently, you can generate for SQLite, SQL Server and MySql databases for which the packages are already available on the NuGet.
<br/>
<br/>
## Usage
### Minimal APIs 
- Create an empty .NET 6.0 **ASP.NET Core Web API** project.
- Remember to uncheck **Use controllers (uncheck to use minimal APIs)** checkbox.
- Remove all code related to **WeatherForecast** API.
- Add dependency from NuGet to **QuickDBS.API** and either **QuickDBS.SQLite**, **QuickDBS.SQLServer** or **QuickDBS.MySQL**.
- Add `using QuickDBS;` to the **Program.cs** file. 
- Before `var app = builder.Build();` line, add the following code:

        // Use SQLite or MySQL if that's what you want
        var db = new SQLServer("databasename");

        // Inject QuickDBS service for APIs
        builder.Services.AddSingleton<IQuickDBS>(db);

        // Create a LoggerFactory for logging from APIs
        builder.Services.AddSingleton<ILogger>(
                LoggerFactory.Create(b => b.AddConsole())
                .CreateLogger("QuickDBS_Minimal_Api"));

        // Remove the following line once APIs are generated.
        APIs.CreateMinimalAPIs(db);   

- Run the project once so that the Models and the APIs are generated.
- Remove or comment the `APIs.CreateMinimalAPIs(db);` line so that it doesn't keep on repeating the generation process.
- After the `app.UseHttpsRedirection();` line, add the following and resolve any namespace issues. 
        
        app.UseQuickDBSApiEndPoints();

- That's it. Now, you should have all the models in the Models folder and APIs in the APIs folder. Run the project and start using the Minimal APIs.
---
### Controllers based APIs 
- Create an empty **ASP.NET Core Web API** project.
- Add dependency from NuGet to **QuickDBS.API** and either **QuickDBS.SQLite**, **QuickDBS.SQLServer** or **QuickDBS.MySQL**.
- Add `using QuickDBS;` to the **Startup.cs** file. 
- In the **Startup.cs** class, add the following in the **ConfigureServices** method

        // Use SQLite or MySQL if that's what you want
        var dbServer = new SQLServer("databasename");

        // Inject QuickDBS service for APIs
        services.AddSingleton<IQuickDBS>(dbServer);

        // Remove the following line once APIs are generated.
        APIs.Create(dbServer);   

- Run the project once so that the Models, Controllers and the Web APIs are generated.
- Remove or comment the `APIs.Create(dbServer);` line so that it doesn't keep on repeating the generation process.
- That's it. Now, you should have all the models in the Models folder and controllers in the Controllers folder. Run the project and start using the Web APIs.
