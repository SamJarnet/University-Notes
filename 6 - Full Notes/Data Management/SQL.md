29-12-2024 17:55

Status:

Tags: [[Data Management]] [[Database Systems]]


# SQL

#### What is SQL?
- SQL: Structured Query Language
- Specified a Data Definition Language (DDL)
	- Tables and views (virtual tables)
	- Convert a data model to a (physical) database
- Specifies a Data Manipulation Language (DML)
	- Programmatic data manipulation
	- Declarative (desired result)
	- INSERT, DELETE, UPDATE or retrieve (SELECT) data
- Provides Administration commands
- Can support:
	- Referential integrity
	- Transactions
	- Checks keys for consistency
	- Access control
	- Concurrent access

#### SQLite:
- All of the database is contained inside a single file
- Perfect for when you need a simple database on the go, without needing to run a fully fledged out database server (such as SQL server, MySQL, etc) 
	- Small
	- No configuration
	- Serverless - no background process/server
	- Lightweight
	- Efficient
	- Supports most SQL and some extensions
	- Cross-platform
	- Open source
- More basic than alternatives
	- It's just a file
	- Not good for larger operations
	- Not multi-user
	- No concurrency 
	- Not client/server
	- Lacks some SQL features

#### Introducing some SQL 
 - Definition - DDL 
	 - CREATE TABLE 
	 - ALTER TABLE 
	 - DROP TABLE 
 - Manipulation - DML 
	 - SELECT 
	 - INSERT 
	 - UPDATE
	 - DELETE


#### Join Types 
- JOIN (or INNER join): returns just rows with matching keys (join column values) 
- LEFT join: returns all rows from left (first) table, whether they match a row in the second table or not 
- RIGHT join: returns all rows from right (second) table, whether they match a row in the first table or not 
- FULL OUTER join: Returns all rows from both tables, whether they match or not
- ![[Pasted image 20241229180700.png]]

Creating Indexes 
- CREATE INDEX ...
- ON ... (...)
- DROP INDEX ...
# References