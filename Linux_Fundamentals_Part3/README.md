# Linux Fundamentals Part3

Power-up your Linux skills and get hands-on with some common utilities that you are likely to use day-to-day!

Nov 24, 2021

#### Task 1: Introduction
- Let's proceed!
  - `no answer needed`

#### Task 2: Deploy Your Linux Machine
- I've logged into the Linux Fundamentals Part 3 machine using SSH and have deployed the AttackBox successfully!
  - `no answer needed`

#### Task 3: Terminal Text Editors
- Create a file using Nano
  - `no answer needed`
- Edit "task3" located in "tryhackme"'s home directory using Nano. What is the flag?
  - I just used `cat task3` to get the flag or you can use nano editor if you want

#### Task 4: General/Useful Utilities
- Ensure you are connected to the deployed instance (MACHINE_IP)
  - `no answer needed`
- Now, use Python 3's "HTTPServer" module to start a web server in the home directory of the "tryhackme" user on the deployed instance.
  - `no answer needed`
- What are the contents?
  - You just have to use the `python3 -m http.server` in the tryhackme box then-
  - You need to `wget http://10.10.80.99:8000/.flag.txt` in your linux then you just have to `cat .flag.txt` to view the text file.
- Use Ctrl + C to stop the Python3 HTTPServer module once you are finished.
  - `no answer needed`

#### Task 5: Processes 101
- Read me!
  - `no answer needed`
- If we were to launch a process where the previous ID was "300", what would the ID of this new process be?
  - `301`
- If we wanted to cleanly kill a process, what signal would we send it?
  - `SIGTERM`
- Locate the process that is running on the deployed instance (10.10.80.99). What flag is given?
  - Just use `ps aux` to view the processes and then you can find the flag.
- What command would we use to stop the service "myservice"?
  - `systemctl stop myservice`
- What command would we use to start the same service on the boot-up of the system?
  - `systemctl start myservice`
- What command would we use to bring a previously backgrounded process back to the foreground?
  - `fg`

#### Task 6: Maintaining Your System: Automation
- Ensure you are connected to the deployed instance and look at the running crontabs.
  - `no answer needed` 
- When will the crontab on the deployed instance (10.10.80.99) run?
  - `@reboot` | I just get it by using `crontab -e` and it is on the last part 

#### Task 7: Maintaining Your System: Package Management
- Since TryHackMe instances do not have an internet connection...this task only requires you to read through the material.
  - `no answer needed`

#### Task 8: Maintaining Your System: Logs
- Look for the apache2 logs on the deployable Linux machine
  - `no answer needed`
> You just have to cat the access.log.1 in the `/var/log/apache2` to get the answer in the following questions.
- What is the IP address of the user who visited the site?
  - `10.9.232.111`
- What file did they access?
  - `catsanddogs.jpg`

#### Task 9: Conclusions & Summaries
- Terminate the machine deployed in this room from task 2. 
  - `no answer needed`
- Continue your learning in other Linux-dedicated rooms.
  - `no asnwer needed`
