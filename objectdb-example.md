## ObjectDB example

Open or Create and Open ObjectDB connection to the folder on the file system. The database name can be absolute path which will create in the location as the absolute path else it will create in the current working folder as the executable file is.
```
var db = new QuickDBS.ObjectDB(@"C:\MyObjectDB");
```
We will use the following ```Person``` class example for demonstrating the use of ObjectDB.
```
public class Person
{
    public Int64 Id { get; set; }
    public string Name { get; set; }
    public double Income { get; set; }
    public DateTime DateOfBirth { get; set; }
}

```
Create a Person record in the Person collection. The result will be the last insert Id of the collection which will be unique.
```
var id = db.Create<Person>(new Person {
  Name = "Rahul",
  Income = 5000,
  DateOfBirth = new DateTime(2000, 01, 01)
});
```
Get the person record having Id = 1 from the Person collection.
```
var person = db.GetById<Person>(1);
person.Name = "Rahul Hadgal";
person.Income = 10000;
```
Update the income for person selected in the above example, from 5000 to 10000 and change name to Full Name.
```
var result = db.UpdateById<Person>(person);
```
Get all records from Person collection
```
var people = db.GetAll<Person>();
```
Delete a person by Id = 1 from the Person collection.
```
var result = db.DeleteById<Person>(1);
```
