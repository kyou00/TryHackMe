OWASP Juice Shop

December 8, 2023 

```
jim@juice-sh.op -tryhackme123
admin@juice-sh.op - admin123
mc.safesearch@juice-sh.op - Mr. N00dles
```

#### Task 1 - Open for business!

- Once the machine has loaded, access it by copying and pasting its IP into your browser; if you're using the browser-based machine, paste the machines IP into a browser on that machine.
	- `No answer needed`

#### Task 2 - Let's go on an adventure!

- Question #1: What's the Administrator's email address?
	- `admin@juice-sh.op`

- Question #2: What parameter is used for searching? 	
	- `q`

- Question #3: What show does Jim reference in his review?
	- `Star Trek`

#### Task 3 - Inject the juice

- Question #1: Log into the administrator account!
	- `32a5e0f21372bcc1000a6088b93b458e41f0e02a`

- Question #2: Log into the Bender account!
	- `fb364762a3c102b2db932069c0e6b78e738d4066`

<details>
Steps:
Just put this in the username when you intercept the POST request in the website using burp
	
```
' or 1=1--
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/369f4d0f-42aa-46fa-858e-ec042aea0a53)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/975d3c27-abba-4198-8784-6a1d1bc7e30d)

Then just click forward to log in as admin.

-----------------------------------------------------------------

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/5ee55031-39ce-4b9b-b1c1-9d1c00591c7a)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/c18573cb-6ec6-450b-adb6-5b40eb65b8ad)

Now we are log in as bender user. 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/92e09a41-a9e2-4594-bdad-ca38be5a37f4)

 	
</details>

#### Task 4 - Who broke my lock?!

- Question #1: Bruteforce the Administrator account's password!
	- `c2110d06dc6f81c67cd8099ff0ba601241f1ac0e`

- Question #2: Reset Jim's password!
	- `094fbc9b48e525150ba97d05b942bbf114987257`

<details>
Steps:
First you have to intercept the login credintials for the admin which you will have to enter the email address first

Then we have to brute force it using the burpsuite tool 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/2ede055a-932c-4b90-9a40-ae96873da1be)

Then we will input the possible passwords / password list for us to know what is the password of user admin.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/9bb0f232-f9dc-45d9-8d6b-6b8a1bf3ec2a)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/cded44f3-3d55-4049-a97f-c11c18c3f07f)

As we can see above the length of the admin123 is different from the rest which means this could be the password for user admin

Then just log in as admin using that password

</details>

#### Task 5 - AH! Don't look!

- Question #1: Access the Confidential Document!
	- `edf9281222395a1c5fee9b89e32175f1ccf50c5b`

- Question #2: Log into MC SafeSearch's account!
	- `66bdcffad9e698fd534003fbb3cc7e2b7b55d7f0`

- Question #3: Download the Backup file!
	- `bfc1e6b4a16579e85e06fee4c36ff8c02fb13795`

<details>
Steps
	
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/4e5dfc08-f2aa-48ba-925b-be0846beefc1)

</details>

#### Task 6 - Who's flying this thing?

- Question #1: Access the administration page!
	- `946a799363226a24822008503f5d1324536629a0`

- Question #2: View another user's shopping basket!
	- `41b997a36cc33fbe4f0ba018474e19ae5ce52121`

- Question #3: Remove all 5-star reviews!
	- `50c97bcce0b895e446d61c83a21df371ac2266ef`

<details>
Steps
Just log in as admin user that go to the developer tools then sources

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/e0429a5c-eb88-495b-93cd-c0157eb9c8b1)

You will find a directory to the administration page 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/807661d5-f37e-4106-baf5-c442dd8d64cf)

----------------------------------------------------------

Try to intercept the basket page

![image](https://github.com/kyou00/tryhackme-writeups/bassets/92074685/eb71ea44-ce4d-43c6-a496-f7199426a6ab)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/ba24ba75-b7e0-4511-a665-dd695483e267)

Then just forward forward the page

After a few forward using burp

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/c149441b-803d-45aa-938b-8a0312576326)

You can now see there is a basket number /rest/basket/1 which means that 1 is your baskter

Try changing it to 2 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/b9bd23ee-ce41-4570-b530-555222c8cf8b)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/e3a24096-e612-439e-9bd0-42377f82fe23)

You can now see the basket of number 2 / user 2

</details>

#### Task 7 - Where did that come from?

- Question #1: Perform a DOM XSS!
	- `9aaf4bbea5c30d00a1f5bbcfce4db6d4b0efe0bf`

- Question #2: Perform a persistent XSS!
	- `149aa8ce13d7a4a8a931472308e269c94dc5f156`

- Question #3: Perform a reflected XSS!
	- `23cefee1527bde039295b2616eeb29e1edc660a0`

<details>
Steps:
Just put this in the search box 

```
<iframe src="javascript:alert(`xss`)"> 
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/02993b92-f43d-4cc1-aa61-cba8b64352ea)

Then you can easily XSS attack to the site

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/c928c19a-b924-455f-81df-a9c9c0fd64b6)

------------------------------------------------------

Go to the last ip login in the website

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/f1ddf96d-0c76-45aa-a095-ce441bb0c557)

Then you have to logout but make sure that burp intercept the logout request

Then we will change the header for that GET request 

We will inject a persistent XSS attack to the server

```
True-Client-IP

<iframe src="javascript:alert(`xss`)">
```
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/6028bbe1-6a42-476c-9fbf-76854c16713f)

As we login a admin then go to the last login page we can now see the XSS attack

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/76440748-0973-44c8-993d-182fa0d64ff3)

</details>

#### Task 8 - Exploration!

- Access the /#/score-board/ page
	- `7efd3174f9dd5baa03a7882027f2824d2f72d86e`
