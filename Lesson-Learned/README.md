# Lesson Learned?

December 17, 2023

---------------------------

- What's the flag?
	- `THM`


<details>
Steps:
Visit the website and you will see the login page. 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/e8d3445b-2c55-4d50-a55a-0acfd34936a4)

Then we will intercept the login credentials using the burpsuite tool.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/3d8304b6-b9dc-4d1e-ac67-35ba7dcc8a31)

We could use hydra to guess for the username that exist in the database, so we can login.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/3cf4fef3-5eeb-4ff0-85b3-2571313467b9)

```
hydra -L ~/Downloads/xato-net-10-million-usernames.txt -p asdf 10.10.157.124 http-post-form "/:username=^USER^&password=^PASS^:Invalid username and password."
```

-------------------------------------------------------
-L for the username 

-p is for the password which we just put a random letters 

10.10.157.124 is the IP address of the website

http-post-form is the HTTP method that has been used.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/0fc232ca-ad45-47f1-8b66-35bc18ce5b7d)

/ is the directory where the username and password goes

username=^USER^ is the username list that has been provided

password=^PASS^ is the password list that has been provided

Invalid username and password is the error message for the wrong credentials

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/3c856a20-2ff1-4d95-b401-d7c8237f1898)

--------------------------------------------------------

Now we know the usernames that we can use we can now proceed to SQL injection.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/5bd49c30-3416-453f-a9a8-2c059b0e2dfb)

We can use this SAFE SQL injection by Tib3rius

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/301bb13e-0b6c-43dd-b230-ddbc564e82f1)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/31ff5559-5aa2-4127-b5af-ec1123e36293)

```
kelly';-- -
```

As we login the credentials we are now in the page 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/801777b7-f700-4599-8268-1bf242dc9abc)

</details>
