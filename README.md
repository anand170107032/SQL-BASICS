# SQL Basics

### What is relaional database management systems and non relational database management system?
Relational database management systems (RDBMS) use tables to store data (MySQL) and non-relational database maqnagement systems do not use tables to store data (NoSQL)

### What is SQL?
Sql stands for structural query language. We can use sql to access and manipulate data in relational database management systems (RDBMS). <br/>
A database often contains one or more tables. The tables can be broken down into **records (rows)** and **fields (col)**.

### Most used keywords in SQL
Query   | Function
--------|--------------------------------------
|SELECT | extracts data from a database
|UPDATE | updates data in a database
|DELETE | deletes data from a database
|INSERT INTO | inserts new data into a database
|CREATE DATABASE | creates a new database
|ALTER DATABASE | modifies a database
|CREATE TABLE | creates a new table
|ALTER TABLE | modifies a table
|DROP TABLE | deletes a table
|CREATE INDEX | creates an index (search key)
|DROP INDEX | deletes an index

Note: Sql Keywords are NOT Case-sensitive

### SELECT keyword
This keyword is used to select data from databases. The selected data is returned in the form of a table. Consider the "Customers" table below 

CustomerID |	        CustomerName  	     |   ContactName
-----------|-------------------------------|---------------------
1          |         Alfreds Futterkiste	 |  Maria Anders	
2	         |         Ana Trujillo          |  Emparedados
3	         |         Antonio Moreno        |	Antonio Moreno	
4          |         Thomas                |  Hardy
5	         |         Berglunds snabbköp	   |  Christina Berglund	


```sql
SELECT * from Customers;
```
The above command will return the full table.

```sql
SELECT CustomerID, CustomerName from Customers;
```
The above command returns the following table

CustomerID	|        CustomerName  	         	
------------|---------------------
1           |        Alfreds Futterkiste	    	
2	          |        Ana Trujillo            
3	          |        Antonio Moreno        		
4           |        Thomas                  
5	          |        Berglunds snabbköp

### SELECT Distinct Keyword
The SELECT DISTINCT statement is used to return only distinct (different) values. Consider the table below

City	      |        State  	         	
------------|---------------------
Kanpur      |        UP	    	
Varanasi	  |        UP            
Dispur	    |        Assam        		
Guwahati    |        Assam                  
Hyderabad	  |        Telangana

```sql
SELECT DISTINCT State from table
```
This command will return the following column

|State|
|------|
|UP|
|Assam|
|Telangana|

```sql
SELECT DISTINCT State, City from table
```
This command will return the following table

City	      |        State  	         	
------------|---------------------
Kanpur      |        UP	    	            
Dispur	    |        Assam        		              
Hyderabad	  |        Telangana

### WHERE Keyword

```sql
SELECT Col1, Col2
FROM table
where condition
```

#### Examples

```sql
SELECT * from table
WHERE City = 'Hyd'
```

```sql
SELECT * from table
WHERE NOT City = 'Hyd'
```

```sql
SELECT * from table
WHERE City = 'Hyd'
AND id = 1
```

```sql
SELECT * from table
WHERE City = 'Hyd'
OR id = 1
```

### Operators in WHERE Clause

OPERATOR | DESCRIPTION
---------|------------
=        | EQUAL
<>       | NOT EQUAL
BETWEEN  | Between a certain range
IN       | To specify multiple possible values for a column
LIKE     | To Search for a pattern
NOT      | Not equal
MOD(dividend, divisor)| For calculating remainders

```sql
SELECT * from table
WHERE ID in (1, 2)
```

```sql
SELECT * from table
WHERE ID BETWEEN (1, 10)
```
NOTE: In the range (1, 10), 1 and 10 are inclusive

### ORDER BY Keyword

ORDER BY Keyword is used to sort the selected records

```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

The above query first sorts the records in ascending order wrt Country, if two countries are same, then it sorts the record in descending order wrt CustomerName

### INSERT INTO

This keyword is used to insert records in database

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

Example
```sql
INSERT INTO Customers (CustomerName, City, Country)
VALUES('Mike', 'Dubai', 'UAE');
```
In the remaining columns, values will be null

### NULL Keyword
```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```

```sql
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```
Always use IS NULL to look for NULL values.

### UPDATE Keyword
```sql
UPDATE table_name
SET col1 = value1, col2 = value2
WHERE Condition
```

### DELETE Keyword
```sql
DELETE FROM table_name
WHERE Keyword
```

### SQL SELECT TOP Keyword
Selects top k records
```sql
SELECT TOP number|percent col1, col2, col3
FROM table_name
WHERE condition
```

### SQL MIN, MAX, COUNT, AVG, SUM
```sql
SELECT MIN(COL1)
FROM table_name
where condition
```

### MEDIAN
```sql
SELECT ROUND(MEDIAN(col), 4)
FROM TABLE
```
**Note**: The median query works for oracle database only, round function rounds the median upto 4 decimals

Same syntax for other functions
Count gives us the number of records selected

### SQL LIKE Keyword

OPERATOR | DESCRIPTION
---------|-------------
%        | zero or one or more characters
_        | one character
\#        | represents any single numerical character. (2\#5) can mean 205, 215,.....295
\[]       | Represents any single character. a[bd]c can mean abc, adc
^        | Represents character which are not in brackets a[^bd]c means aac, acc, aec...etc
\-        | Represents range of characters a[b-z]c means abc, acz, adz, aez....azz

```sql
SELECT * 
FROM table_name
WHERE Col1 LIKE 'a%n'
```
The above query selects words which start with a and end with n

### SQL Aliases

SQL Aliases are used to give the table or columns of the table a temporary name.
Why are they used? TO MAKE THE COLUMN NAMES MORE READABLE.
This alias will only exist till the duration of the query.

```sql
SELECT col1 AS alias_name
from table_name;

SELECT col1
from table_name AS alias_name

SELECT col1 AS [alias name]
from table_name;
/* if alias name contains space, then use bracket */

SELECT col1 as c1, col2 + ", " + col3 + ", " + col4 as c2
from table_name;
/* column concatenation */

SELECT t1.col1, t2.col1
from table1 as t1, table2 as t2
where condition;
/* selecting data from multiple tables */
```
### SQL JOINS (VERY IMPORTANT)
We can definitely use where instead of joins (There are no performance benefits). But using join makes the query more readable.

The different types of joins are:
1) INNER JOIN: Returns the records which have matching values in both the table.
2) LEFT JOIN: Returns all the left table records plus the matched records in the right table
3) RIGHT JOIN: Returns all the right table records plus the matched records in the left table.
4) FULL JOIN OR FULL OUTER JOIN: Returns all records from both the tables whether they are matched or not.
5) A self JOIN is a regular join, but the table is joined with itself.
```sql
SELECT table1.col1, table2.col2
FROM table1
INNER JOIN table2
ON table1.id = table2.id
```

```sql
SELECT * FROM table1 a
JOIN table2 b ON a.ID = b.ID
JOIN table3 c ON a.ID = c.ID

/* Joining Multiple tables */
```
### SQL FLOOR and CEIL

```sql
SELECT FLOOR(AVG(col1))
FROM TABLE1
```
### SQL REPLACE
```sql
SELECT REPLACE('abcd', 'cd', 'ef')
/* Replaces all occurences of 'cd' with 'ef'.*/
```
```sql
SELECT REPLACE(col1, "ab", "cd")
/* REPLACES all occurences of ab in column 1 with cd. */
``` 
### SQL CASE Statement
```sql
SELECT col1, col2, col3, col4
FROM table_name
ORDER BY
CASE
    WHEN col1 = NULL THEN col2
    WHEN col2 = NULL THEN col3
    ELSE col4
END
```
<https://www.hackerrank.com/challenges/what-type-of-triangle/problem>
### SQL CONCAT
```sql
CONCAT(expression1, expression2, expression3,...)
```
NOTE: This works in MySQL.
<https://www.hackerrank.com/challenges/the-pads/problem>

### SQL substring
```sql
substring(s, 5, 2)
/* selects 2 characters starting from character at index 5 (Note these are 1 based index) */
```
### Group by, aggregates and having clause 
<https://www.youtube.com/watch?v=K2mFsfhLckw>

### Joins
<https://www.youtube.com/watch?v=KTvYHEntvn8> <br/>

Inner join vs natural join: <https://www.geeksforgeeks.org/difference-between-natural-join-and-inner-join-in-sql/> <br/>

### Primary and foreign keys
Primary keys uniquely identify a record. There can be multiple primary keys for a table. <br/>
Foreign keys are used to link 2 tables together. A foreign key in one table is a primary key in another table. <br/>

Primary Key | Foreign Key
------------|--------------
Primary key is used to uniquely identify a record in the table | Foreign key is used to link two tables. A foreign key in one table is generally a primary key in other table
Only 1 primary key is allowed | Multiple foreign keys are allowed
Primary key does not allow null values | Foreign keys allow null values

### Data-types in sql
1) int
2) varchar(n): A string with maximum n characters
3) char(n): A string with n characters (Fixed Length)
4) float
5) numeric(p, d): A floating number with p - d digit(s) before the decimal point and d digit(s) after the decimal point

### Create table
```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```
### Create table using other table
```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
```
### SQL Union
The UNION operator is used to combine the result-set of two or more SELECT statements. <br/>

Each SELECT statement within UNION must have the same number of columns <br/>
The columns must also have similar data types <br/>
The columns in each SELECT statement must also be in the same order <br/>

UNION selects only distinct records <br/>
To allow Duplicate records use UNION ALL <br/>

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

### Any and All
The ANY and ALL operators are used with a WHERE or HAVING clause. <br/>
The ANY operator returns true if any of the subquery values meet the condition. <br/>
The ALL operator returns true if all of the subquery values meet the condition. <br/>

https://www.w3schools.com/sql/sql_any_all.asp>

### insert into tables
```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```
