# Advent of Cyber 2023

Day 6 Memory corruption Memories of Christmas Past

-----------------------------------

- If the coins variable had the in-memory value in the image below, how many coins would you have in the game?
	- `1397772111`

- What is the value of the final flag?
	- `THM`


<details>
Steps:

Question 1:

Just use the rapidtables hex to decimal to get the value that they asking. 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/0c29bd97-6c23-41aa-91fc-1f390b7e9669)

-----------------------------------------

Question 2:

As we know that we need to buy the star in the shop which is letter D.

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/3f08f841-d88e-4d69-8d66-1b6b6e872534)

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/ddbd3000-34b8-4245-9411-a58867094544)

If we change our name to "AAAABBBBCCCCDDDD" we will have a huge amount of coins. 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/935ef910-4915-44e4-9466-c1ad223e1dd2)

If we change our name to "AAAABBBBCCCCDDDDEEEEFFFFGGGGHHHHIIIIJJJJKKKKd" we can now get a star in our inventory. 

Since the value of the star in the inv_items is letter - d 

![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/ee23a953-3aba-4b58-b808-9362337db3f7)

</details>
