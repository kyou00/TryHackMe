# Advent of Cyber 2023

[Day 8] Disk forensics Have a Holly, Jolly Byte!

-------------------------------

- What is the malware C2 server?
	- `mcgreedysecretc2.thm`

- What is the file inside the deleted zip archive?
	- `JuicyTomaTOY.exe`

- What flag is hidden in one of the deleted PNG files?
	- `THM`

- What is the SHA1 hash of the physical drive and forensic image?
	- `39f2dea6ffb43bf80d80f19d122076b3682773c2`

<details>
Steps:
Just open the secretchat.txt you can see the server that they are using. Use the text viewer.

 ![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/a346460c-6740-4983-9bf4-bbaa4420d72a)

----------------------------------------
Just open the deleted zip and use the view automatically in the upper column.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/d23f845e-05c4-48cf-832d-4d22c60e6ab9)

--------------------------------------
If you just use Ctrl+F, you can search for THM{ in the portrait.png. Just use the hex viewer.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/14c6e9fc-3a82-4ea7-88ae-59c74c913b43)

-----------------------------
You will see the SHA1 hash when it is done verifying..

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/b9cf58ac-f48a-4dcd-8d88-bde742a889a6)

</details>
