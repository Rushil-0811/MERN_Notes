look into SOLID design, ensure whatever u write follows these principles.
 MySQL, vector databases, graph db, neo4j
 postgres,

Learn SQL - Online SQL Terminal - Practice SQL Querys

imp query statements and clauses

where - kinda the if condition
 LIKE to search for words, BETWEEN for the range
 Update - update column
 Set - set data of column 
 is null - chck wehter null or not
 select 
 concat - connect and combine two columns
 AS
 select concat (x column, ' ', y column) as xy column from table name

to get and display combined data from two different tables, u need to have a common column, 
 we use JOIN in such cases,

SELECT table1.column1, table2.column2
 FROM table1
 JOIN table2 
 ON table1.common_column = table2.common_column;

INNER JOIN Records with matching values in both tables.
 LEFT JOIN All records from the left table, plus matches from the right
 RIGHT JOIN All records from the right table, plus matches from the left.
 FULL JOIN All records when a match exists in either table.

count (*) - count all rows
 select * - return all columns
 year (column_name) - 
 you use MAX with select
 col_name = select max (col_name) from tab_name
 is not null, is null
 group by col_name - makes separate groups and aggregate functions like count, act on each group
 count (*) as whatever_name
 the above will return the count as whatever name u select
 distinct

select distinct 
 from table
 where column name =