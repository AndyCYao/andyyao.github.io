### CMPT 354 Database Management Winter 2017

## ER Diagrams and Relational Diagram 
*ER Diagrams* are for concepts, it is used for abstract grouping of entities and relationships
*Relational Diagram* is for logical modeling, tends to be drawn when the ER Diagram is already fleshed out.

## Entity 
	Weak entity are those that depends on a foreign entity to identiy itself. AKA child entity that depends on the parent entity

	Strong entity, those that have their own primary key

## Covering Constraint and Overlap Constraint
	Pertains to the ISA relation.
	*Covering Constraint* - Does every Employee have to be a contractor, or temp?
	*Overlap Constraint* - Can contractor or temp overlap? ie. Can the employee be both

## Keys
	- Super key are set of candidate keys.
	- Candidate keys are column or columns that uniquely identifies the entries in an entity
	- Primary key is the minimal candidate key. 

## Database 
	- This is a physical storage of data, we will be installing relational databases, which is a part of DBMS (database management system)

	- The purpose of a DB is to faciliate access/ storing data. key things to note is to protect data from concurrent users, crash recoveries, etc. 

	-a schema is a way to describe data

## SQL
	- we have DDL, data definition language, which are the CREATE, DROP, DELETE, keywords
	- DML, data manipulation language, which includes
	keywords such as SELECT, UPDATE, DELETE etc. 

## ACID
	- Databases must maintain 'ACID'
	- Atomic - groups of transaction must all pass or all fail, if fail, a log is used to unroll the changes. 
	- Consistent - After each transaction, the DB is in consistent state.
	- Isolation - Concurrency control to allow multi user
	- Durability - the database must not be corruptible and lose information

'''
INSERT INTO tableName(a, b, c, d)
VALUES (1,2,3,4)

CREATE VIEW ViewName 
(SELECT ...)

DROP VIEW

LIKE (case insensitive)

UNION - joins two select queries, note fields have to be the same

INTERSECT - 

EXCEPT

Relational Algebra's Set division can be translated to SQL like so

e.g.  Find sailors who’ve reserved all boats
SELECT  S.sname
FROM  Sailors S
WHERE  NOT EXISTS 
            ((SELECT  B.bid
                 FROM  Boats B)
             EXCEPT
             (SELECT  R.bid
               FROM  Reserves R
               WHERE  R.sid=S.sid))

Find Entity that have only 1 attribute
e.g. Find the snames of suppliers who supply only red parts.
Select S.sid from Suppliers S
where ‘Red’ = ALL (select Parts.color 
		from Catalog, Parts
		where Catalog.sid = S.sid and Parts.pid = Catalog.pid )


'''

a = Any {a,3} 	True
a  = All  {a,3} 	False
a = Any 	{}	False
a = All	{}	True
