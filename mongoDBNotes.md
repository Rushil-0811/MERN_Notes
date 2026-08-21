monogodb uses no sql format
data is stored in various forms besides sql table
related data stored as a single document
single document = single row and table in sql
uses bson, binary notation, 

document is a gorup of field value pairs to represent an object
colletion is a group of documents
database is a group of collections

commands
mongosh to start powershell in downloads, mongosh on current system
cls to clear
exit to stop
show dbs to show all databases
use admin - to swithc or create a new database
fill db to show it on show dbs

db.createcollection("students") - creates collection for school
on db school to make it appear in show dbs

use school - creates new db with name school

to insert data into the school db, we insert to the students collection

school> db.students.insertOne({name:'abc', age:30})

the below command will return everything inside of the studnet collection
school> db.students.find()

insert multiple documents into the student collection
its basically a collection of objects inside of an array
schoool> db.students.insertMany([{}, {}, {}])
this method is just how to insert documents using the shell method
you can do the same using the compass

data types
string - "series of text within doubled quotes"
can also contain numbers
integer is a whole number
double - decimal 
booleans - true or false
null - no value
arrays - ["this will contain", "multiple data"]

finding and sorting
.find to find all in the document, sort by name 1 to sort in ascending order
name will be -1 to reverse sorted order
.limit(1) will return just 1 value
basically u get the collection name, attatch . functions to the collection
db.students.find().sort({name:1})

.find method
name of db and add .find()
db.students.find({name:'abc'}) 
passing object to find is to get specific
db.students.find({gpa:'4'})
can use more than one filter
filter separated by commas, this is basically the where query from sql
it has a projection parameter as well
.find({}, {}) the second object is projection
.find({}, {name:true}) to return just the name 
.find({}, {_id:false, name:true, gpa:true})
basically .find format is 
.find({query}, {projection})