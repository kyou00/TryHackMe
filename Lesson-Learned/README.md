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
hydra -L ~/Downloads/xato-net-10-million-usernames.txt -p asdf 10.10.172.59 http-post-form "/:username=^USER^&password=^PASS^:Invalid username and password."
```

-L for the username 

-p is for the password which we just put a random letters 

10.10.172

</details>
