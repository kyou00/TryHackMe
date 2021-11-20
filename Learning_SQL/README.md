# Learning SQL Commands

Just taking some notes about different commands.

---------------------------------------------

- select * from users;
	- Selecting all columns from users table

- select username,password from users;
	- Selecting username and password column from users table

- select * from users LIMIT 1;
	- Selecting only one row from the users table

- select * from users LIMIT 2,1
	- Skipping two rows and returning one row

- select * from users where username='admin';
	- Selecting all columns from users table where the username is equal to admin

- select * from users where username != 'admin';
	- Selecting all columns from users table where the username is not equal to admin

- select * from users where username='admin' or username='jon';
	- Selecting all columns from users table where the username is equal to admin or jon

- select * from users where username='admin' and password='p4ssword';
	- Selecting all columns from users table where the username is equal to admin and password is equal to p4ssword

- select * from users where username like 'a%';
	- Selecting all columns from users table where the username starts with the letter a

- select * from users where username like '%n';
	- Selecting all columns from users table where the username ends with the letter n

- select * from users where username like '%mi%';
	- Selecting all columns from users table where the username containing the characters mi within them.
