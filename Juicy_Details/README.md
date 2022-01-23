Walkthrough about Pickle Rick

January 23, 2022

---------------------------------------------

First, we have to download the files. 

## Task 1: Introduction
- Are you ready?
	- `I am ready!`

## Task 2: Reconnaissance

We just have to look for the tools in the file "access.log" to find the tools that have been used regarding the atk.

- What tools did the attacker use? (Order by the occurrence in the log)
	- `nmap,hydra,sqlmap,curl,feroxbuster`


This is the directory that is vulnerable to the brute-force attack and the tool that was used is hydra. Which we did see in the file.

- What endpoint was vulnerable to a brute-force attack?
	- `/rest/user/login`


Then this directory is vulnerable to SQL Injection and they used sqlmap to take advantage this vulnerability.

- What endpoint was vulnerable to SQL injection?
	- `/rest/products/search`

This is the parameter that has been used upon the attack basically the parameter comes after the "?" thing in the url, for example

```
http://url.com/rest/products/search?q=1%20AND%209700%3D9700--%20jEIr HTTP/1.1" 200
```

You can see the "?"

- What parameter was used for the SQL injection?
	- `q`


Then, we can see in the file that there is service that the attacker can take advantage of and it is a directory seen by feroxbuster tool.
There are certain files that can be stored in the ftp service basically it can be retrieve if it was leave open.

- What endpoint did the attacker try to use to retrieve files? (Include the /)
	- `/ftp`


## Task 3: Stolen Data

If we will use the hint button in the room we can see the answer and from there we can understand/comprehend the statement.

- What section of the website did the attacker use to scrape user email addresses?
	- `products reviews`


This is being based on the http 200 request in the brute-force attack and the tool that have been used is Hydra, we can see there that it is been successfull because the server returns http 200 which means it is ok.

- Was their brute-force attack successful? If so, what is the timestamp of the successful login? (Yay/Nay, 11/Apr/2021:09:xx:xx +0000)
	- `Yay,11/Apr/2021:09:16:31 +0000`

This can be seen in the query of sqlmap attack.

- What user information was the attacker able to retrieve from the endpoint vulnerable to SQL injection?
	- `email,password`


We can see this in the "vsftpd.log" file in the lowest part.

- What files did they try to download from the vulnerable endpoint? (endpoint from the previous task, question #5)
	- `coupons_2013.md.bak, www-data.bak`

This is service that we discuss earlier and the service uses the port 21 which is ftp
We can retrieve files there if it is open and use the username anonymous

- What service and account name were used to retrieve files from the previous question? (service, username)
	- `ftp,anonymous`

The service ssh is same as the ftp but it is enhanced since we can see all the files and the ssh is pretty secured. Also, we can directly connect to the server or the computer by the ssh port and we can access of all the file by just this service.

The ssh service works in the port 22

- What service and username were used to gain shell access to the server? (service, username)
	- `ssh,www-data`