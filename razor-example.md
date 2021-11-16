# QuickDBS.Razor

A tiny library that generates Razor pages for a given model that includes listing, adding new, updating existing and deleting from available records. The model is connected to the table using any of the supported QuickDBS databases.

## Usage / Examples

Follow the steps to generate UI pages for your models.
- Create a new ASP.Net Core Web App (Razor pages).
- Add NuGet packages **QuickDBS.Razor** and any of your preferred **QuickDBS** databases package which you want to use.
- Open **Program.cs** or **Startup.cs** depending upon the .NET template you are using.
- If you are using latest template, you have to add the following code in **Program.cs** after the existing Services that are already added. In case of older templates, add these lines in **Startup.cs** where services are configured.
```
//Open connection to database. You can use SQLite or MySQL if that's you choice instead of SQLServer.
var databaseService = new SQLServer("databasename");

//Add dependency to database in the created pages.
builder.Services.AddSingleton(databaseService);

//Generate UI for models. Each line creates UI pages for each model/table.
//Note: You need to remove or comment the following lines, once you run
// the project and the UI pages are created. This is a one-time process.

RazorUI.BuildFor<Student>(true);  //Student is both model and table in database.
RazorUI.BuildFor<Admission>(true);  //Admission is both model and table in database.

// If required, keep adding the models that needs the UI pages to be generated as shown above.
```
