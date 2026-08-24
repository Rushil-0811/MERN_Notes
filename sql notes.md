sql notes
key words are case insensitive, end with semi colon to end a sql command

sql is case insensitive, at least select is 
select * from table ;
write functions in caps to distinguish from column names and all

CREATE DATABASE test;

CREATE TABLE test (
test_column INT
);

ALTER TABLE test, this is to add a column to a table already created
ADD another_column VARCHAR(255); ,var char is variable character array
DROP TABLE test;

CREATE TABLE bands( 
id INT NOT NULL AUTO_INCREMENT,
band_name VARCHAR(255) NOT NULL,
PRIMARY KEY (id)
);

primary identifier for the table, in above case id column is the primary key.

CREATE TABLE albums( 
id INT NOT NULL AUTO_INCREMENT,
album_name VARCHAR(255) NOT NULL,
release_date INT ,
band_id INT NOT NULL,
PRIMARY KEY (id),
FOREIGN KEY (band_id) REFERENCES bands(id)
);

need to reference the data in the band table from inside of the album table, can use the id column which is represented as band_id,
this band_id is a foreign key


INSERT INTO bands (band_name)
VALUES ("IRON MAIDEN");

INSERT INTO bands(band_name)
VALUES('ABC') , ('XYZ'); 

insert is to add values to the columns, above are some examples for that

now to query the data which we have added so far, select *, the * selects every column

SELECT * FROM bands;

SELECT * FROM bands LIMIT 2;

SELECT band_name FROM bands;
SELECT id as "ID", band_name AS bandName FROM bands;
the above is called aliasing

SELECT * FROM bands ORDER BY band_name; 

INSERT INTO albums (album_name, release_date, band_id)
VALUES ('ALbum NAMe', 1985, 1),
('Album anem 2', 2019, 2),
('test album', NULL, 4);

SELECT * FROM albums

SELECT DISTICT album_name FROM albums

UPDATE albums 
SET release_date  = 2017 
WHERE id=1;

SELECT * FROM albums 
WHERE release_date < 2010;

SELECT * FROM albums
WHERE band_name LIKE '%er%' OR band_id =2;

anything before er and anything after er, that band_name will return

DELETE FROM albums
WHERE id=5;

now time to join the tables so that queries can be written for joint data, making queries powerful, allowing to create relations b/w/ data

SELECT * FROM bands 
JOIN albums ON bands.id - albums.band_id;

this basic method of join is also called INNER JOIN

INNER JOIN combines data of tables which have a match and only return that data

LEFT JOIN lists everything from the first side which in this case will be the bands table.

Aggregate functions

SELECT AVG(release_year) FROM albums
GROUP BY band_id;

SELECT b.name AS band_name, COUNT(a.id) AS num_albums FROM bands AS b
LEFT JOIN albums AS a ON b.id = a.band_id
GROUP BY b.id
HAVING num_albums=1;

having vs where, having happens after grouping, where happens before
renaming the column names and all is called aliasing i guess
express odes not allow to use/access body data, wee need to use middleware for this.
redirect changes the URL.
app.use(express.json())
app.use(express.urlencode())

query parmas
req.query.name