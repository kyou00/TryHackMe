# Advent of Cyber 2023


------------------------------------------------------------

#### Day 3: Brute-forcing - Hydra is Coming to Town

- Using crunch and hydra, find the PIN code to access the control system and unlock the door. What is the flag?
	- `THM`

First you need to a list for possible 3 digits combination.
```
crunch 3 3 0123456789ABCDEF -o 3digits.txt
```
<details>
The command above specifies the following:

3 the first number is the minimum length of the generated password

3 the second number is the maximum length of the generated password

0123456789ABCDEF is the character set to use to generate the passwords

-o 3digits.txt saves the output to the 3digits.txt file
</details>

Then you will navigate to the login page of the site. 
Go to the view source code. 
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/fd71f2cc-4db5-42f7-8f7a-b635088abb1d)

```
hydra -l '' -P 3digits.txt -f -v 10.10.179.47 http-post-form "/login.php:pin=^PASS^:Access denied" -s 8000
```
<details>
The command above will try one password after another in the 3digits.txt file. It specifies the following:

-l '' indicates that the login name is blank as the security lock only requires a password

-P 3digits.txt specifies the password file to use

-f stops Hydra after finding a working password

-v provides verbose output and is helpful for catching errors

10.10.44.85 is the IP address of the target

http-post-form specifies the HTTP method to use

"/login.php:pin=^PASS^:Access denied" has three parts separated by :

/login.php is the page where the PIN code is submitted

pin=^PASS^ will replace ^PASS^ with values from the password list

Access denied indicates that invalid passwords will lead to a page that contains the text “Access denied”

-s 8000 indicates the port number on the target	
</details>
