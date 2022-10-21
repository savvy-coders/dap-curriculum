# SQL

---

# What is a database

## According to Oracle:

A database is an organized collection of structured information, or data, typically stored electronically in a computer system. A database is usually controlled by a database management system (DBMS). Together, the data and the DBMS, along with the applications that are associated with them, are referred to as a database system, often shortened to just database.  

Before the adoption of RDBMS systems flat files were often used for each table.

In Excel each tab could be thought of as a table and the workbook itself as a database.

In a modern DBMS the meta-data is also in tables, row, and columns. 

---

# SQL 

## Structured Query Language

Structured Query language came along as a methodology to simplify data retrieval from relational databases. 
SQL's advent created a paradigm shift away from rows to set based operations. 
It changed everything.

---

# Database Types

## Relational

- Data is stored in tables and the relationships between the tables can be defined and enforced by the DBMS. 
- Transactional integrity, if a transaction will update more than one table then all updates must succeed or the transaction will be rolled back. 
- Relational databases are most commonly used for transactional systems. 

---

## NoSQL

- Data can be stored in many different formats in a NoSQL environment. 
	- Common formats include: tables, json, and XML and BLOB
- Grew out of the need to capture tremendously high volume data flows
- Commonly used in experimental analytics.

---

# Standard Data Types

Char - a fixed length string
Varchar - variable length string
Integer - whole numbers (can be signed or unsigned)
Float - a floating point number (used for scientific calculations - do not use for financial calculations)
Decimal - a fixed-point number


https://www.w3schools.com/sql/sql_datatypes.asp


NULL - is not a datatype

---

# SQLite Datatypes

## Storage Classes and Datatypes

Each value stored in an SQLite database (or manipulated by the database engine) has one of the following storage classes:

-   **NULL**. The value is a NULL value.
-   **INTEGER**. The value is a signed integer, stored in 0, 1, 2, 3, 4, 6, or 8 bytes depending on the magnitude of the value.
-   **REAL**. The value is a floating point value, stored as an 8-byte IEEE floating point number.
-   **TEXT**. The value is a text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE).
-   **BLOB**. The value is a blob of data, stored exactly as it was input.

https://www.sqlite.org/datatype3.html

---

# Exercise One - SQLite 

Prerequisites: 
- SQLite - https://www.sqlite.org/download.html
- DB Browser for SQLite - https://sqlitebrowser.org/dl/

Many IDEs exist for manipulating SQL databases
- HeidiSQL
- VS Code Extensions
- Commercial products like dbForge

---

## New Database

From the SQLite terminal:
1. Open SQLite.exe
	1. Microsoft does not recognize this program and will warn you.
2. You will start in "in memory" mode - this database is destroyed when the program closes.
3. Use `.backup practice` to save the file to disk.

---

## Create tables

### Departments
- DepartmentId Int Primary Key
- DepartmentName Text

``` sql 
create table Departments(DepartmentId int, DepartmentName text)`
```

https://www.sqlite.org/lang_createtable.html

---

## Create tables 2

### Subjects
- SubjectId Int Primary Key
- SubjectName Text
- DepartmentId Int

### Students
- StudentId Int Primary Key
- StudentName Text 

### Grades
- StudentId Int Primary Key
- SubjectId Int
- Grade Int

_You might want to wait on creating these... there may be a better way in another slide or two..._

---

## Inserting Data

``` sql
insert into Departments(DepartmentId, DepartmentName) values(1, "IT");

insert into Departments(DepartmentId, DepartmentName) values(2, "Arts"),(3,"Spanish");

insert into Departments(DepartmentId, DepartmentName) values(4, "History"),(5,"Science"),(6, "Band"),(7,"StudyHall");
```

https://www.sqlite.org/lang_insert.html

---

# Exercise 2 - DBBrowser

## Open DB Browser
- Open Database and select `practice.sqlite`
- Click on create table and type out the column names, datatype, and attributes for each of the remaining tables. 
- DB Browser creates the code for you:

``` sql
CREATE TABLE "Subjects" (
	"SubjectId"	INTEGER,
	"SubjectName"	TEXT,
	"DepartmentID"	INTEGER,
	PRIMARY KEY("SubjectId")
);
```

## Do this for the remaining tables
- Students and Grades

---

## Inserting Data - DB Browser

### Subjects

| SubjectId  | SubjectName | DepartmentID |
| ---------- | ----------- | ------------ |
| 1 | Python      | 1            |
| 2 | Tableau						| 1 |
| 3 | Painting						| 2 |
| 4 | Spanish for travelers			| 3 |
| 5 | Spanish 200					| 3 |
| 6 | NASA during the Shuttle Era	| 4 |
| 7 | Chemistry						| 5 |
| 8 | Biology						| 5 |
| 9 | Jazz							| 6 |
|10 | Independant Study				| 7 |

---

### Students

| StudentId | StudentName |
| --------- | ----------- |
| 1         | Sarah       |
| 2         | Maria       |
| 3         | Brandon     |
| 4         | Stephen     |
| 5         | Ronnie      |
| 6         | Matthew     |
| 7         | Mariah      |
| 8         | Ray         |
| 9         | Brandi      |
| 10        | Hunter      |
| 11        | Sophia      |

---

### Grades

| SubjectId | StudentId | Grade |
| --------- | --------- | ----- |
| 1         | 1         | 85    |
| 3         | 1         | 90    |
| 6         | 1         | 78    |
| 2         | 2         | 99    |
| 4         | 2         | 87    |
| 7         | 2         | 77    |
|           |           |       |
...

There would be many more records to enter here but I think everyone is ready to move on.

---

# Break

## Some questions to think about:
1. Where are the relationships?
2. Can you think of a reason why I am about to use the word, "Intersection"
3. Why doesn't the Grades table have a primary key
	1. What makes this table special?
	2. Could / Should it have a primary key

---

# Welcome Back

---

# Testing your tables:

``` sql

select * from Departments; 

select * from Subjects;

select * from Students;

select * from Grades;

```

---

# Updating data

Stephen only let's his mom call him that... we need to change his name to Steve.

``` sql

select * from students;

```


What is his id number in your system? In mine he is 4.

``` sql

update students set StudentName = 'Steve' where StudentId = 4;

```

Rerun your query - did his name get changed?

---

# Dropped class

Brandon isn't cutting it in the Jazz class and has decided to drop.

``` sql

delete from grades where StudentId = 3 and SubjectId = 9;

```


---

# Changing a Table Definition

``` sql

alter table Subjects add column CreditHours Int;

update subjects set CreditHours = 3 where SubjectId <> 10;

select * from subjects;

alter table Subjects drop column CreditHours;

```

---

# Making results Human friendly

So far we have been content using the computer friendly id columns to work through our examples. 

Let's take a look at a better way of working with query results.

## Welcome to inner joins 

``` sql

select * 
	from Grades g
	inner join Students s
		on g.StudentId = s.StudentId
	inner join Subjects C --classes
		on g.SubjectId = c.SubjectId
		;

```


---

# Can we make this better?

``` sql

select s.StudentName
	,c.SubjectName
	,g.Grade 
	from Grades g
	inner join Students s
		on g.StudentId = s.StudentId
	inner join Subjects c --classes
		on g.SubjectId = c.SubjectId
		;

```

---

# Maybe one more tweak

``` sql


select s.StudentName as "Student Name"
	,c.SubjectName as "Class"
	,g.Grade as 'Result'
	from Grades g
	inner join Students s
		on g.StudentId = s.StudentId
	inner join Subjects C --classes
		on g.SubjectId = c.SubjectId
		;

```

---

# Review

The last query looks pretty good, right? Easy to read, has just what makes sense to the humans. But what if we want all students regardless of enrollment in a class?

## Welcome to left joins

``` sql

select s.StudentName as "Student Name"
	,c.SubjectName as "Class"
	,g.Grade as 'Result'
	from Students s
		left join Grades g
			on s.StudentId = g.StudentId
		left join Subjects C --classes
			on g.SubjectId = c.SubjectId
		;


```

---

# What about RIGHT joins?

## Just don't
- Your future self will never forgive you if you right a query with both left and right joins
- I almost never see right joins in the wild
- Technical Debt is real - some say code is a liability. 
- Venn Diagrams.

https://www.w3schools.com/sql/sql_join.asp

---

# Filtering - Using the Where Clause

## Like - pattern matching

``` sql

select StudentName 
	from Students s
	where s.StudentName like 'm%';

select StudentName 
	from Students s
	where s.StudentName like '%n';


```

https://www.w3schools.com/sql/sql_select.asp
https://sqlite.org/lang_select.html

---

# SQLite GLOB

I doubt anyone will need this - and it is only implemented in SQLite:

``` sql

SELECT 1 where 'Mariah' GLOB 'm%';

SELECT 1 where 'Mariah' LIKE 'm%';


```

GLOB is case sensitive and uses Unix style wildcards.

---

# Using Where ... And

``` sql

select s.StudentName
	,s.StudentId
	from Students s
		where s.StudentID > 5
			and s.StudentName like 'm%';
			
```

---

# Using Where ... Or

``` sql

select s.StudentName
	,s.StudentId
	from Students s
		where s.StudentID > 5
			or s.StudentName like 'm%'

```

---

# Use parenthesis in your where clauses


``` sql

select s.StudentName
	,s.StudentId
	from Students s
		where s.StudentID > 5
			and s.StudentName like 'm%'
			or s.StudentName like 'n%'
			
```
 
 Might not be what you are looking for...

``` sql 


select s.StudentName
	,s.StudentId
	from Students s
		where s.StudentID > 5
			and (s.StudentName like 'm%'
			or s.StudentName like 's%');

```

---

# Filtering based on a range of values

``` sql 

select s.StudentName as "Student Name"
	,c.SubjectName as "Class"
	,g.Grade as 'Result'
	from Grades g
		inner join Students s
			on g.StudentId = s.StudentId
		inner join Subjects C --classes
			on g.SubjectId = c.SubjectId
	where g.Grade between 80 and 90;

```

Most MS SQL Server coders frown on this practice because the boundaries are included.

---

# Try this instead

``` sql 

select s.StudentName as "Student Name"
	,c.SubjectName as "Class"
	,g.Grade as 'Result'
	from Grades g
		inner join Students s
			on g.StudentId = s.StudentId
		inner join Subjects C --classes
			on g.SubjectId = c.SubjectId
	where g.Grade >= 80 
		and g.Grade <= 90;

```

This code is more easily read and understood - your future self will thank you. 

---

# Pickup at slide 28