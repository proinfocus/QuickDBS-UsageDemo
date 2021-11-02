## SQL Server example

To open SQL Server connection to the database directly. The following code connects to the default SQLExpress instance with Trusted Connection and to the database **databaseName**. You could provide the complete connection string instead of just database name, in case you need to connect to remote machine or require secure connection with username and password.
```
var db = new QuickDBS.SQLServer("databaseName");

or

string connectionString = "Server=SERVERNAME; Database=SOMEDATABASENAME; User=USERNAME; Password=PASSWORD";
var db = new QuickDBS.SQLServer(connectionString);
```
Create a table from a Person class. The result will be true if created and false if failed or not-created.
```
public class Person
{
    public Int64 Id { get; set; }
    public string Name { get; set; }
    public double Income { get; set; }
    public DateTime DateOfBirth { get; set; }
}

var result = db.CreateTable<Person>();
```
Create a Person record in the Person table create above. The result will be the last insert Id of the table which will be unique.
```
var id = db.Create<Person>(new Person {
  Name = "Rahul",
  Income = 5000,
  DateOfBirth = new DateTime(2000, 01, 01)
});
```
Get the person record having Id = 1 from the Person table.
```
var person = db.GetById<Person>(1);
person.Name = "Rahul Hadgal";
person.Income = 10000;
```
Update the income for person selected in the above example, from 5000 to 10000 and change name to Full Name.
```
var result = db.UpdateById<Person>(person);
```
Get all records from Person table
```
var people = db.GetAll<Person>();
```
Custom Query with conditions
```
var people = db.Query<dynamic>("SELECT Id, Name, Income FROM Person WHERE
                                Income >= @MinIncome AND Income <= @MaxIncome",
                                new { MinIncome = 6000, MaxIncome = 12000 });
```
Delete a person by Id = 1 from the Person table
```
var result = db.DeleteById<Person>(1);
```
