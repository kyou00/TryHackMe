# Advent of Cyber 2023

------------------------------------------------------------

#### Day 2: Log Analysis - O Data, All Ye Faithful

- Open the notebook "Workbook" located in the directory "4_Capstone" on the VM. Use what you have learned today to analyse the packet capture.
	- `No answer needed`

- How many packets were captured (looking at the PacketNumber)?
	- `100`

Just scroll down to the file csv.

- What IP address sent the most amount of traffic during the packet capture?
	- `10.10.1.4`

```
df['Source'].value_counts()
```

- What was the most frequent protocol?
	- `ICMP`

```
df['Protocol'].value_counts()
```
