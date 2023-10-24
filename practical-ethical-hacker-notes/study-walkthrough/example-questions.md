# Example Questions

* What is the IP of the Windows X machine?
* Find the IP address of the machine which is running the RDP?
* What is the version of the Linux Kernel?
* How many Windows machines are there?
* Find the OS name of the machine which is running MySQL database?
* What is the password for user X of the FTP server?
* Find the HTTP method that poses a high risk to the application example.com?
* What is user X's IBAN number?
* Which user X's phone number?
* Find the password of the wordpress user “Mario”?
* What is the password hidden in the .jpeg file?
* Rogue AP suspect, crack your password using capture.cap
* Discovery RAT in Network and acess computer to recovery secret.txt
* Identify IoT Message using capture.cap
* Find the attacker IP address who has launched the DOS attack?
* Identify FQDN of Domain Controller
* Find the username/password from the pcap file, which is in plain text?
* Find the number of machines that were used to iniate the DDOS attack?
* Find the file name which is tampered by comparing the hashes which is given in the /hashes folder?
* Decrypt the volume file using veracrypt?
* Decode the file which is encoded in DES(ECB) format?
* Perform deep scan on the elf and obtain hash of the file with highest entropy value.
* Connect to the Server remotely using the credentials give by RDP?
* Find the executable's Entry point (Address)
* Extract the information from the SDcard of the Android User?

#### CEH Practical Exam Questions Examples:

* Find the machines running MSSQL ?
* Find the machines running Remote Desktop ?
* Find DOS attacker ips from pcap file ?
* Identify modifed text files , (hint : check integrity)
* Crack MD5 Hashes.
* Find attacker's username from machine?
* Find contact details of Jenny ? (hint : dump the table using sqlmap)
* Find username password ? (hint : Bruteforce using wpscan)
* Use hydra to crack password
* some question on Gui RATs tools
* 4 5 problems on cryptography and steganography. Prepare all the Windows Gui tools from cryptography section. practice system exploitation using metasploit,

Exam is pretty good, you can surf internet , open any documents pdfs you want , make sure you have stable internet connection, parrot os is extremely laggy .

Tools : NMAP SQLMap Hydra Wireshark Veracrypt Hashcalc Dirb Steghide Searchsploit Hashcat John WPSCAN Metasploit



[Sample Questions](https://github.com/0xParth/CEH-Practical-Guide/blob/main/README.md#sample-questions)

1. Which username was tampered? ( You need to solving by comparing Hash values)
2. Wordpress Username Enumeration!
3. Retrieve Database names ( SQLi)
4. How many machines are there? ( NMAP)
5. Phone number of User X? ( Metasploit/Parameter Tampering)
6. What is the hidden text in X.jpeg (STEGHIDE)
7. Password crack for VCRYPT
8. IP Address/ Version of Running windows Server.

***

[Some of the commands used by me](https://github.com/0xParth/CEH-Practical-Guide/blob/main/README.md#some-of-the-commands-used-by-me)

1. hydra -l root -P passwords.txt \[-t 32] ftp \[ [https://securitytutorials.co.uk/brute-forcing-passwords-with-thc-hydra/](https://securitytutorials.co.uk/brute-forcing-passwords-with-thc-hydra/)]
2. hydra -L usernames.txt -P pass.txt mysql
3. hashcat.exe -m hash.txt rokyou.txt -O
4. nmap -p443,80,53,135,8080,8888 -A -O -sV -sC -T4 -oN nmapOutput 10.10.10.10 \[[https://www.stationx.net/nmap-cheat-sheet/](https://www.stationx.net/nmap-cheat-sheet/)]
5. wpscan --url [https://10.10.10.10/](https://10.10.10.10/) --enumerate u
6. netdiscover -i eth0 \[ [https://www.100security.com.br/netdiscover](https://www.100security.com.br/netdiscover) ]
7. john --format=raw-md5 password.txt \[ To change password to plain text ]







