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
* Find DOS attacker ips from pcap file ?
* Identify modifed text files , (hint : check integrity)
* Crack MD5 Hashes.
* Find attacker's username from machine?
* Find contact details of Jenny ? (hint : dump the table using sqlmap)
* Find username password ? (hint : Bruteforce using wpscan)
* Use hydra to crack password
* some question on Gui RATs tools
* 4 5 problems on cryptography and steganography. Prepare all the Windows Gui tools from cryptography section. practice system exploitation using metasploit,
* If you get any questions related to netbios, SMB use metasploit.

**Others exam questions:**

* How many machines are active? Use netdiscover
* Which machine has FTP Server open? Use nmap
* Find 2 secret files using FTP? brute force FTP username and psw.
* Find out phone number of Web application user? Use sqlmap
* Brute force Wordpress  website user's psw? Use wpscan
* Decode .hex file? Use Cryptool
* Which machine started DOS attack? DDOS attack happened on which IP? Find out http crediantls from PCAP file? Use wireshark
* Decode the given text using given secret? Use BCTextEncorder
* Calculate SHA1 hash of a text? Use Hashcalc
* Decrypt the hidden vulume and find secret file? Use Veracrypt.
* Crack the given hash? Use hashes.com
* Find secret hidden int he image/file? Usen openstego/snow
* Find a secret file in Android? Use ADB
* Send data to another machine (firewall blocked)? Use Covert TCP.

1. Which username was tampered? ( You need to solving by comparing Hash values)
2. Wordpress Username Enumeration!
3. Retrieve Database names ( SQLi)
4. How many machines are there? ( NMAP)
5. Phone number of User X? ( Metasploit/Parameter Tampering)
6. What is the hidden text in X.jpeg (STEGHIDE)
7. Password crack for VCRYPT
8. IP Address/ Version of Running windows Server.

***

#### Some of the commands used by me <a href="#user-content-some-of-the-commands-used-by-me" id="user-content-some-of-the-commands-used-by-me"></a>

1. hydra -l root -P passwords.txt \[-t 32] ftp \[ [https://securitytutorials.co.uk/brute-forcing-passwords-with-thc-hydra/](https://securitytutorials.co.uk/brute-forcing-passwords-with-thc-hydra/)]
2. hydra -L usernames.txt -P pass.txt mysql
3. hashcat.exe -m hash.txt rokyou.txt -O
4. nmap -p443,80,53,135,8080,8888 -A -O -sV -sC -T4 -oN nmapOutput 10.10.10.10 \[[https://www.stationx.net/nmap-cheat-sheet/](https://www.stationx.net/nmap-cheat-sheet/)]
5. wpscan --url [https://10.10.10.10/](https://10.10.10.10/) --enumerate u
6. netdiscover -i eth0 \[ [https://www.100security.com.br/netdiscover](https://www.100security.com.br/netdiscover) ]
7. john --format=raw-md5 password.txt \[ To change password to plain text ]

### Domande - tools

4\) WireShark

I have perfomed DDos to practice Download from here : https://drive.google.com/drive/folders/10YvNHem8NgjLJCy1XvdYqU5cDJKlo To find DOS (SYN and ACK) : tcpflagssyn - 1 , tcp.flags.syn 1 and tcp.flags.ack 0 To find passwords : http.request.method POST&#x20;

5\) SqlMap

sqlmap -u "http://vmw.moviescope.com/viewprofile.aspx?id=l" —dbs \[ Copy the cookie from website, mysql -U qdpmadmin -h 192.168.1.8 -P passwod \[ If you have logins credentioals I&#x20;

6\) OWASP ZAP

&#x20;7\) Hashcat

hashcat -m 0 -a 0 hash.txt passwordlist.txt -m 0: MD5 hash mode -a 0: Dictionary attack mode hash.txt txt file containing hash in a compliant format passwordlist.txt: dictionary file containing passwords in plain text

&#x20;8\) John

john —format-raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt&#x20;

9\) Hydra

hydra -L /user.txt -P (password.txt ftp://172.0.16.21&#x20;

10\) Veracrypt&#x20;

11\) Crypttool&#x20;

12\) Hash Calculator&#x20;

13\) MD5 Calculator&#x20;

14\) PhoneSploit&#x20;

15\) MetaSploit

If you get any questions related to netbios, SMB use metasploit.

16\) BCTextEncoder

### Tools

NMAP SQLMap Hydra Wireshark Veracrypt Hashcalc Dirb Steghide Searchsploit Hashcat John WPSCAN Metasploit&#x20;

**Windows based Commands which will help you to find the answers.**\
**1)** **net user** — For Domain Users Enumeration\
**2)** **snow.exe** -C -p “password” stegfile.txt\
**3)** **type** C:\path.txt — It displays the content of the path.txt file.\
**4)** **dir**\
**5)** **cd**\
**6)** **hostname**\
**7)** **whoami**\
**8)** **PWd**

Tools Used da Technology Hacks (video):

**in Parrot Box:**

netdiscover, nmap, hydra, john the ripper, wpscan, sqlmap, ADB\
hashcat PhoneSploit Metasploit

**In Windows Box:**

Wireshark, Hashcalc, Veracrypt, BCTextEncoder, Cryptool, Snow, OpenStego

\
 <a href="#effd" id="effd"></a>
-------------------------------
