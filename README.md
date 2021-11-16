# QuickDBS
"QuickDBS" short for "Quick Database Services" is a library to perform CRUD operations on SQL Server, MySql and SQLite databases quickly and easily. It works near to the metal so it is as good as using ADO with the simplicity and ease.

In addition to database services, it has support libraries to generate Web APIs, Razor Pages and Blazor UI pages dynamically and connect them via supported QuickDBS databases and that it further.

## NuGet Packages

The following are the links to the NuGet packages. You can either use Package Manager in Visual Studio or CLI in VS Code.

Download QuickDBS for SQLite from [QuickDBS.SQLite](https://www.nuget.org/packages/QuickDBS.SQLite/) or

Download QuickDBS for SQL Server from [QuickDBS.SQLServer](https://www.nuget.org/packages/QuickDBS.SQLServer/) or

Download QuickDBS for MySql from [QuickDBS.MySQL](https://www.nuget.org/packages/QuickDBS.MySQL/)

Download QuickDBS.API to generate Web APIs dynamically from the QuickDBS supported databases from [QuickDBS.API](https://www.nuget.org/packages/QuickDBS.API/)

Download QuickDBS.Blazor to generate Blazor UI pages dynamically from the models that are connected to the QuickDBS supported databases from [QuickDBS.Blazor](https://www.nuget.org/packages/QuickDBS.Blazor/)

Download QuickDBS.Razor to generate Razor pages dynamically from the models that are connected to the QuickDBS supported databases from [QuickDBS.Razor](https://www.nuget.org/packages/QuickDBS.Razor/)

## Features
- Single line to connect to the database.
- Create Tables from your Classes in the database.
- Generate Classes under **Models** folder in your project from the tables of the selected database.
- Read records using *GetById*, *GetAll*, *GetAllWhere* methods.
- Add records using *Create* and *CreateMany* methods.
- Update records using *UpdateById* and *UpdateMany* methods.
- Delete records using *DeleteById* and *DeleteMany* methods.
- Get custom records by custom return queries using *Query* method.
- Execute custom non-returning queries using *NonQuery* method.
- Execute queries under **Transactions** using *CreateTransaction* and once done, commit them using *CommitTransaction* or rollback using *RollbackTransaction*

Note: Class Name = Table Name, Property Names = Field Names. Always **Id** is the Auto-incrementing, Primary Key having Int64 type. It ignores the properties which are custom/user created. To illustrate it, in the following example, the property **Hobby** is ignored and other 2 properties are used to create the table as well as perform CRUD operations.
```
public class Person
{
    public Int64 Id { get; set; }
    public string Name { get; set; }
    public Hobby MyHobby { get; set; } // This property is ignored automatically.
}
```

## Usage
All SQL Server, MySql and SQLite libraries of QuickDBS works very much identical with just the change in the connection string. It makes switching between SQL Server, MySql and SQLite easier.
It also has the ability to group different database executions under a transaction using **CreateTransaction** method following with either **CommitTransaction** or **RollbackTransaction** methods as required.

The following is a simple example of how the transaction can be used.
```
var db = new QuickDBS.SQLite("quickdbs-test.db3");
db.CreateTransaction();

// Create Record
// Update Record
// Read Record
// Delete Record

db.RollbackTransaction();
```
The above code connects to a SQLite db and a Transaction is started by executing ```db.CreateTransaction();``` Then a series of CRUD operations are undertaken and finally when the code reaches ```db.RollbackTransaction();``` it reverts back to the original state. If you replace it with ```db.CommitTransaction();``` it will retain the changes in the database.

By default, ```CreateMany```, ```UpdateMany```, ```DeleteMany``` and ```NonQuery``` methods works exclusively with Transaction without you defining it. Multiple changes to records are either committed when whole transaction is complete or rolled back when something goes wrong.

## Power Features
Apart from CRUD operations, this can be used to generate classes from the connected database using ```GenerateClassesForTables``` and create tables from the classes you have into the selected database using ```CreateTable``` methods.


---

## Examples
- For SQLite database examples, goto [sqlite-example](sqlite-example.md)
- For SQL Server database examples, goto [sqlserver-example](sqlserver-example.md)
- For MySql database examples, goto [mysql-example](mysql-example.md)
- For Web APIs generation example, goto [api-generation](api-generation.md)
- For Blazor UI generation example, goto [blazor-ui-creator](blazor-ui-creator.md)
- For Razor UI generation example, goto [razor-example](razor-example.md)
