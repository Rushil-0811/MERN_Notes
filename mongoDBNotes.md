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

update documents in mongodb
db, name of collection
can updateone or updatemany

db.students.updateOne(filter, update)
set replaces value of a field, the update is to replace the selected filter
the set is used to define what parameter of the document is to be updated of the selected filter
better to update via object id, IDs are unique to each document
db.students.updateOne({name:'Rushil'}, {$set:{fulltime:trure}})
db.students.find(_id:ObjectId(the id in the db))

updatemany method
updates many documents at once
db.students.updateMany(filter, update)
db.students.updateMany({}, {$set:{modify a field}})
keeping filter empty will update every item in the document
students.updateMany({fulltime:{$exists:false}}, {$set:(modify)})

delete documents 
deleteONe and deleteMany
db.students.deleteOne(filter, )
similar to update one and update many
db.students.deleteMany({some filter, maybe the value of a key})
can delete complete fields using deleteMany
deleteMany({registrationDate:{$exists:false}})
exists and set operators are used for this update and delete

operators
denoted with $ sign
$ comparison operators
$ne:{name}
every value that is not equal to the name passed inside {}

less than and less than equals to
students.find({age:{$lt:20}})
returns any results with age less than 20
lte is less than equal whihc includes 20 as well
lot of operators like this, look em up I guess

this covers crud for mongodb
we connect mongo with express that about it

in operator to find everything in the array 
.find({name:{$in:["any name u wanna find, name 1, name 2"]}})
nin is not in, opposite of in, return documents that arent mentioned in the array

these are all comparison operators

logical operators
and, not, nor , or
and - check if 2 expressions are true
operators preceede with a $, : after the operator is called, []
db.students.find({$and: [{fulltime:true}, {age:{$lte:22}}]})
or - any of the condition is true 
nor - both need to be false
not - reverses what is being looked for

indexes 
quick lookup of a field, but it takes up more memory
data stored as a b-tree
.find is a linear search
lookup speed can be improved using indexes
db.students.createIndex({name: 1})
name
db.students.getIndex
db.students.dropIndex

collections
collection is group of documents
database is group of collections

look up interview questions as well later on