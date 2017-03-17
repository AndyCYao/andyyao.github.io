---
layout: default
title: "Database Management"
code: "CMPT 354"
semester: "Winter 2017"

---
## CMPT 354 Database Management Winter 2017

### ER Diagrams and Relational Diagram 
*ER Diagrams* are for concepts, it is used for abstract grouping of entities and relationships
*Relational Diagram* is for logical modeling, tends to be drawn when the ER Diagram is already fleshed out.

### Entity 
Weak entity are those that depends on a foreign entity to identiy itself. AKA child entity that depends on the parent entity

Strong entity, those that have their own primary key

### Covering Constraint and Overlap Constraint
Pertains to the ISA relation.
*Covering Constraint* - Does every Employee have to be a contractor, or temp?
*Overlap Constraint* - Can contractor or temp overlap? ie. Can the employee be both

### Keys
- Super key are set of candidate keys.
- Candidate keys are column or columns that uniquely identifies the entries in an entity
- Primary key is the minimal candidate key. 

### Database 
- This is a physical storage of data, we will be installing relational databases, which is a part of DBMS (database management system)

- The purpose of a DB is to faciliate access/ storing data. key things to note is to protect data from concurrent users, crash recoveries, etc. 

-a schema is a way to describe data

### SQL
- we have DDL, data definition language, which are the CREATE, DROP, DELETE, keywords
- DML, data manipulation language, which includes
	keywords such as SELECT, UPDATE, DELETE etc. 

### ACID
- Databases must maintain 'ACID'
- Atomic - groups of transaction must all pass or all fail, if fail, a log is used to unroll the changes. 
- Consistent - After each transaction, the DB is in consistent state.
- Isolation - Concurrency control to allow multi user
- Durability - the database must not be corruptible and lose information

~~~ sql
	
	INSERT INTO tableName(a, b, c, d)
	VALUES (1,2,3,4)

	CREATE VIEW ViewName 
	(SELECT ...)

	DROP VIEW

	LIKE (case insensitive)

	UNION - joins two select queries, note fields have to be the same

	INTERSECT - 

	EXCEPT
~~~

Relational Algebra's Set division can be translated to SQL like so

e.g.  Find sailors who’ve reserved all boats
~~~ sql
SELECT  S.sname
FROM  Sailors S
WHERE  NOT EXISTS 
	    ((SELECT  B.bid
	      FROM  Boats B)
	        EXCEPT
	            (SELECT  R.bid
	               FROM  Reserves R
	               WHERE  R.sid=S.sid))
~~~

Find Entity that have only 1 attribute
e.g. Find the snames of suppliers who supply only red parts.

~~~ sql
	Select S.sid from Suppliers S
	where ‘Red’ = ALL (select Parts.color 
			from Catalog, Parts
			where Catalog.sid = S.sid and Parts.pid = Catalog.pid )
~~~

a = Any {a,3} 	True

a  = All  {a,3} 	False

a = Any 	{}	False

a = All	{}	True

## Exam 2 Prep Notes

### Aggregate Operators
Operates on tuple sets, keywords include 
- COUNT(), 
- COUNT(DISTINCT())
- SUM()
- AVG()
- MAX()
- MIN()
Note when doing aggregation, need to include 'GROUP BY' keyword

the HAVING keyword acts as a filter to the aggregate clause. 

### Null Values
can be interpreted as 
- Value Unknown(eg, rating has not yet been assigned)
- Value inapplicable ( no spouse's name)
- Value withheld (phone number)

Rule For Null:
- an arithmetic operator with at least one NULL argument always returns NULL
- Comparison of a NULL value to any second value returns a result o UNKNOWN
therefore, a selection returns only these tuples that makes the condition in the WHERE clause TRUE, those with unknown or false do not qualify. 
As part of 3 value logic (Ture False Unknown)

TRUE AND UNKNOWN = UNKNOWN

FALSE AND UNKNOWN = FALSE

FALSE OR UNKNOWN = UNKNOWN

NOT UNKNOWN = UNKNOWN

~~~ sql
SELECT * 
FROM t1
WHERE col_1 > 5
OR col_1 < 5
OR col_1 = 5
~~~
Any record where col_1 has NULL will not be returned in the above query

### Outer Joins
SQL outer joins include NULL values

~~~ sql
SELECT *
FROM a LEFT OUTER JOIN b
ON a.id = b.id
~~~
LEFT OUTER JOIN would show dangling tuples from left input table. (null is filled for all attribute of right input)

RIGHT OUTER JOIN does the same but from right table's perspective

FULL OUTER JOIN shows dangling tuples from both input table

### Security 

~~~ sql
-- ex1
GRANT SELECT, INSERT, DELETE 
ON Reserves 
TO Yuppy 
WITH GRANT OPTION

-- ex2
GRANT UPDATE(rating) ON Sailors TO
Leah
~~~
user yuppy can now select, insert, and delete, and also grant other people these privileges. 

user leah can now update ratings, but can't gran this privilege to other. 

### View
use view when you want more control on whether the user can read, write, execute depending on authorization level.

View is a relation that is stored for use later. 

### Integrity Constraints CHECK and ASSERTION
Types of IC include:
- Domain Constraint (field values must be right type, always enforced)
- Attribute based CHECK (defined in declaration of an attribute, activate on insertion)
~~~ sql
CREATE TABLE ..
... CHECK (col_1 >= 1 AND col_2 <= 30)

-- can also name the check 
CREATE TABLE ...
CONSTRAINT noFoo
CHECK('Foo' <> ANY(SELECT ...))
~~~
	
- Tuple-Based Check (defined in declaration of table, activate on insertion to corrosponding table or update of tuple) 
~~~ sql
CREATE TABLE ...
... CHECK(colA >= colB)
~~~
- Assertion: (defined independently from any table, activate on any modification of any table mentioned in assertion)
~~~sql
CREATE ASSERTION notTooManyReservations
CHECK (10 > ALL (SELECT COUNT(*)
				FROM Reserves
				GROUP BY sid))
~~~
Checks and Assertions are not well supported in SQL.

Check is not in SQL SERVER

Assertion is not supported in postgresSQL

### Triggers
procedures that starts automatically if specificed change occurs in the DBMS.

has 
- Event (activates the trigger)
- Condition (tests whether trigger should run)
- Action

~~~ sql
CREATE TRIGGER youngSailorUpdate
    AFTER INSERT ON SAILORS			/* Event */
    REFERENCING NEW TABLE NewSailors	
    FOR EACH STATEMENT
	   INSERT					/* Action */
		INTO YoungSailors(sid, name, age, rating)
		SELECT sid, name, age, rating
		FROM NewSailors N
		WHERE N.age <= 18;
-- Referencing include
NEW TABLE
OLD TABLE
OLD ROW
NEW ROW
--- Use begin and end to include multiple SQL Statements
~~~
the above inserts young sailors into separate table. 

### Trigger Vs General Constraints
Triggers can be activated in one SQL statement, but with arbitrary order,
trigger can activate other triggers.

trigger is more general than constraints, it can be used to monitor integrity constraints, construct a log, gather database stats. etc. 