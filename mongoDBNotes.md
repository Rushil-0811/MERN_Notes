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
