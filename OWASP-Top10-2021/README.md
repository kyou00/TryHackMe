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

#### Steps: 

1. Go to crackstation.net then paste the md5 hash below

```
5f4dcc3b5aa765d61d8327deb882cf99
```

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

#### Steps:

1. Look around the source code of the site. 