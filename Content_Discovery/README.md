# Content Discovery 

This room gives information about the simple contents of an web application and discussing some sites that can be used for OSINT.

Nov 19, 2021

"Just practicing my writeup skill."

---------------------------------------------

#### Task 1: What is Content Discovery?

- What is the Content Discovery method that begins with M?
	- `Manually`

- What is the Content Discovery method that begins with A?
	- `Automated`

- What is the Content Discovery method that begins with O?
	- `OSINT`

Just read the file.

---------------------------------------------

#### Task 2: Manual Discovery- Robots.txt

- What is the directory in the robots.txt that isn't allowed to be viewed by web crawlers?
	- `/staff-portal`

I get it by entering the http://MACHINE_IP/robots.txt

---------------------------------------------

#### Task 3: Manual Discovery- Favicon

- What framework did the favicon belong to?
	- `cgiirc`

---------------------------------------------

#### Task 4: Manual Discovery- Sitemap.xml

- What is the path of the secret area that can be found in the sitemap.xml file?
	- `/s3cr3t-area`

---------------------------------------------

#### Task 5: Manual Discovery- HTTP Headers

- What is the flag value from the X-FLAG header?
	- Just do the instructions.

---------------------------------------------

#### Task 6: Manual Discovery- Framework Stack

- What is the flag from the framework's administration portal?
	- Just do the instructions.

---------------------------------------------

#### Task 7: OSINT - Google Hacking / Dorking

- What Google dork operator can be used to only show results from a particular site?
	- `site:`

---------------------------------------------

#### Task 8: OSINT - Wappalyzer

- What online tool can be used to identify what technologies a website is running?
	- `Wappalyzer`

---------------------------------------------

#### Task 9: OSINT - Wayback Machine

- What is the website address for the Wayback Machine?
	- `https://archive.org/web/`

---------------------------------------------

#### Task 10: OSINT - Github

- What is Git?
	- `version control system`

---------------------------------------------

#### Task 11: OSINT - S3 Buckets

- What URL format do Amazon S3 buckets end in?
	- `.s3.amazonaws.com`

---------------------------------------------

#### Task 12: Automated Discovery

- What is the name of the directory beginning "/mo...." that was discovered?
	- `/monthly`
- What is the name of the log file that was discovered?
	- `/development.log`

'''
❯ feroxbuster -u http://10.10.146.191 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x log
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.3.3
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://10.10.146.191
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 👌  Status Codes          │ [200, 204, 301, 302, 307, 308, 401, 403, 405, 500]
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.3.3
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 💲  Extensions            │ [log]
 🔃  Recursion Depth       │ 4
 🎉  New Version Available │ https://github.com/epi052/feroxbuster/releases/latest
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Cancel Menu™
──────────────────────────────────────────────────
200       65l      175w        0c http://10.10.146.191/contact
200       51l      152w        0c http://10.10.146.191/news
301        7l       12w      178c http://10.10.146.191/assets
302        0l        0w        0c http://10.10.146.191/customers
200        1l        5w        0c http://10.10.146.191/development.log
301        7l       12w      178c http://10.10.146.191/assets/avatars
301        7l       12w      178c http://10.10.146.191/private
200        1l        4w        0c http://10.10.146.191/monthly
'''