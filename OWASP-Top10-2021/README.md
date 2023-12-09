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
Use burpsuite intruder to change brute force certain possible answers

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/dc955aa5-854b-4aeb-a1c9-c0e77a4290b6)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/c4ff74fa-9915-44d4-8512-8a8fed376132)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/db2062f7-e266-4294-8ce7-6a2ce4d56b0f)


![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/f87e7212-ce6e-45c8-be3a-620d37e0729f)

Then just login to the user joseph using the new password to get the THM
</details>


#### Task 12 - (5) Security Misconfiguration

- Navigate to http://MACHINE_IP:86/console to access the Werkzeug console.
	- `No answer needed`

- Use the Werkzeug console to run the following Python code to execute the ls -l command on the server:
	- `import os; print(os.popen("ls -l").read())`

- What is the database file name (the one with the .db extension) in the current directory?
	- `todo.db`

- Modify the code to read the contents of the app.py file, which contains the application's source code. What is the value of the secret_flag variable in the source code?
	- `THM`

<details>
Steps:

use this command to list the files in the current directory.

```
import os; print(os.popen("ls -l").read())
```

just use the cat command to view the flag from the app.py
```
import os; print(os.popen("cat app.py").read())
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/ef0139f6-c4c3-45a1-a041-024377dfc712)

</details>

#### Task 13 - (6) Vulnerable and Outdated Components

- Read about the vulnerability.
	- `No answer needed`

#### Task 14 - Vulnerable and Outdated Components - Exploit

- Read the above!
	- `No answer needed`

#### Task 15 - Vulnerable and Outdated Components - Lab
	
- What is the content of the /opt/flag.txt file?
	- `THM`

<details>
Steps:

Download the cve from the exploit db for the CSE online bookstore.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/caa85b24-50a8-44c3-939b-c331ffce974f)


Then use that exploit to have remote shell to the server. 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/7ecf0a3d-754b-49bb-af14-73212ec185fb)


Just cat the /opt/flag to view the THM flag.
</details>

#### Task 16 - 7. Identification and Authentication Failures

- I've understood broken authentication mechanisms.
	- `No answer needed`
   
#### Task 17 - Identification and Authentication Failures Practical

- What is the flag that you found in darren's account?
	- `fe86079416a21a3c99937fea8874b667`
   
- Now try to do the same trick and see if you can log in as arthur.
	- `No answer needed`

- What is the flag that you found in arthur's account?
  	- `d9ac0f7db4fda460ac3edeb75d75e16e`
 
<details>
Steps: 
Just create a account that similar to username darren but put space in the front of the letters " darren".
So that you can access the account of darren but imititating his name.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/0d95f90f-5075-491e-8492-05bb19c5fa6d)

</details>

#### Task 18 - (8) Software and Data Integrity Failures

- Read the above and continue!
	- `No answer needed`

#### Task 19 - Software Integrity Failures

- What is the SHA-256 hash of https://code.jquery.com/jquery-1.12.4.min.js?
	- `sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ=`

<details>
Steps: 
Just put the link for the 256 hash integrity.
	
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/8d05f7fe-2976-444a-8392-67927108478e)

</details>

#### Task 20 - Data Integrity Failures

- Try logging into the application as guest. What is guest's account password?
	- `guest`

- What is the name of the website's cookie containing a JWT token?
	- `jwt-session`

- Use the knowledge gained in this task to modify the JWT token so that the application thinks you are the user "admin".
	- `No answer needed`

- What is the flag presented to the admin user?
	- `THM`
<details>.
Steps:
As you can see if we guess the password of user guest we can see his password in the error message.

 ![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/753fc653-f336-46a5-bca7-e2e6580a4e90)

 So just use this password to login to the website as user guest.

 We can see here the session token for user guest.

 ![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/db0573ce-2646-41c7-977e-2648361e49a7)

 You may guess this is encoded using Base64 so we can use the site - https://appdevtools.com/base64-encoder-decoder 
 
 To decode

 ![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/d82c453b-9118-4c5b-ba79-885402735847)

 We can also use the site to encode the modified payload.

 ![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/7e484410-bddd-4b46-9624-570a2127cd51)

 By changing the guest user to admin we can now log in as admin into the site and removing the signature from the cookie.

 ![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/858fa213-8d2a-4cc8-aac8-3daeeadeb4ba)

 ![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/d0d3ea18-782d-463e-bc01-a9f88d275864)

</details>

#### Task 21 - (9) Security Logging and Monitoring Failures

- What IP address is the attacker using?
	- `49.99.13.16`

- What kind of attack is being carried out?
	- `Brute force`

<details>
Just cat the login-logs.txt to view the IP used by attacker

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/9973e98f-29d7-4d54-a33f-8aa4c829b305)

</details>

#### Task 22 - 10. Server-Side Request Forgery (SSRF)

- Explore the website. What is the only host allowed to access the admin area?
	- `localhost`

- Check the "Download Resume" button. Where does the server parameter point to?
	- `secure-file-storage.com`

- Using SSRF, make the application send the request to your AttackBox instead of the secure file storage. Are there any API keys in the intercepted request?
	- `THM`

<details>
Steps:

Download the resume. 

Open netcat

```
nc -lvp 80
```

As we intercept the download button we can see where does the website actually getting the file 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/844d5752-5756-4389-8133-4073b765d78e)

We can manipulate this to our own attack machine so that the traffic will direct to us

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/c655ca7c-1a3e-4d52-9a44-63a2d42f2f92)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/90654b3d-4d36-4bd8-bce2-689270a2c559)

As you can see we actually get the response from the server and we can see the API Key which is the flag

........................

By editing the server to their localhost we can now view their admin page and download the pdf file through that page.

Dont forget the ID in the url since it included in the python script

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/08cd2f53-9473-4e9d-b91e-a46f7679e940)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/0e8a05c1-b873-4158-974c-e9b1e57e74c9)

Just by opening the pdf file we can see the other flag 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/203b6d6b-1d9b-4102-ad09-92719bdb8a9e)

</details>
