# QuickDBS
"QuickDBS" short for "Quick Database Services" is a library to perform CRUD operations on SQL Server and SQLite databases quickly and easily. It works near to the metal so it is as good as using ADO with the simplicity and ease.

Note: **QuickDBS.Console** project is used to test both the libraries. This project can be ignored.

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

Note: Class Name = Table Name, Property Names = Field Names. It ignores the properties which custom/user created. To illustrate it, in the following example, the property Hobby is ignore and other 2 properties are used to create the table as well as perform CRUD operations.
```
public class Person
{
    public Int64 Id { get; set; }
    public string Name { get; set; }
    public Hobby MyHobby { get; set; } // This property is ignored automatically.
}
```

## Usage
Both SQL Server and SQLite libraries of QuickDBS works very much identical with just the change in the connection string. It makes switching between SQL Server and SQLite easier.
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
