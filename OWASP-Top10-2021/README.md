# Owasp Top 10 - 2021

------------------------

#### Task 1 - Introduction

- Read the above.
	- `No answer needed`

#### Task 2 - Accessing Machines 

- Connect to our network or deploy the AttackBox.
	- `No answer needed`

#### Task 3 - (1) Broken Access Control

- Read and understand what broken access control is.
	- `No answer needed`

#### Task 4 - Broken Access Control (IDOR Challenge)

- Read and understand how IDOR works.
	- `No answer needed`

- Deploy the machine and go to http://10.10.49.210 - Login with the username noot and the password test1234.
	- `No answer needed`

- Look at other users' notes. What is the flag?
	- `THM`

Just change the note_id to 0 then you will see the flag.
```
http://10.10.49.210/note.php?note_id=0
```

#### Task 5 - (2) Read the introduction to Cryptographic Failures and deploy the machine.

- Read the introduction to Cryptographic Failures and deploy the machine.
	- `No answer needed`

#### Task 6 - Cryptography Failures (Supporting Material 1)

- Read and understand the supporting material on SQLite Databases.
	- `No answer needed`

#### Task 7 - Read the supporting material about cracking hashes.

- Read the supporting material about cracking hashes.
	- `No answer needed`
<details>
#### Steps: 

Go to crackstation.net then paste the md5 hash below

```
5f4dcc3b5aa765d61d8327deb882cf99
```
</details>

#### Task 8 - Cryptographic Failure (Challenge)

- What is the name of the mentioned directory?
	- `/assets`

- Navigate to the directory you found in question one. What file stands out as being likely to contain sensitive data?
	- `webapp.db`

- Use the supporting material to access the sensitive data. What is the password hash of the admin user?
	- `6eea9b7ef19179a06954edd0f6c05ceb`

- Crack the hash. What is the admin's plaintext password?
	- `qwertyuiop`

- Log in as the admin. What is the flag?
	- `THM`
<details>
#### Steps:
Look around the source code of the site. view-source:http://10.10.11.49:81/

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/cc160a39-6cf7-47e7-a273-9953416c9a65)

You will find a login page. Go to that page.
Then look around the source code again for that page. view-source:http://10.10.11.49:81/login.php

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/7918115f-88b9-4d8a-b4d7-69e2df2bca4a)

View the assets page for that site. Since the comments from login.php was telling us.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/1fae7843-d6ce-439b-b63c-6e624ad57713)

Download the webapp.db then use sqlite3 to that file

```
sqlite3 webapp.db
.tables
PRAGMA table_info(users);
SELECT * FROM users;
```

.table to show the columns in that table
PRAGMA table_info(users); to show the information about the column
SELECT * FROM users; to display the data from the columns

admin:6eea9b7ef19179a06954edd0f6c05ceb

Go to crackstation to crackt this md5 hash

Then login the credentials to login.php as admin you will see the THM

</details>


#### Task 9 - (3) Injection 

- I've understood Injection attacks.
	- `No answer needed`

#### Task 10 - (3.1) Command Injection

- What strange text file is in the website's root directory?
	- `drpepper.txt`

- How many non-root/non-service/non-daemon users are there?
	- `0`

- What user is this app running as?
	- `apache`

- What is the user's shell set as?
	- `/sbin/nologin`

- What version of Alpine Linux is running?
	- `3.16.0`

<details>
Steps:
Just do $(ls) command to show the file in the current directory.
	
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/add045a9-5770-4fc5-aa80-cd8573ad96f6)

Just do $(cat /etc/passwd) to reveal the non-root/non-service/non-daemon, for the user that runs the application, and for the user shell set.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/961dea05-2f02-4f1b-a1d8-874d1d22302e)

Just do $(cat /etc/apline-release) to show the alpine version.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/0da68367-e461-4ad6-8a29-d60eee76935d)

</details>

#### Task 11 - (4) Insecure Design

- Try to reset joseph's password. Keep in mind the method used by the site to validate if you are indeed joseph.
	- `No answer needed`

- What is the value of the flag in joseph's account?
	- `THM`

<details>
Steps:

Navigate to the i forgot password section.



</details>