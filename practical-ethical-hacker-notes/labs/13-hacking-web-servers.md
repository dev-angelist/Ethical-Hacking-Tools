# 13 - Hacking Web Servers

## Module 13 - Hacking Web Servers

<details>

<summary>EMPTY</summary>



</details>

## Web Server Reconnaissance & Footprinting

### Skipfish – WebServer Recon

`skipfish -o /root/test -S /usr/share/skipfish/dictionaries/complete.wl http://10.10.10.12:8080`

\-o path to store output, -S read only word list

### ID Server - Webserver Foot printing

* ID Serve determines the domain name associated with an IP address.
* Click the Server Query tab. In option 1, enter the URL (http://10.10.10.12:8080/CEH)
* Click Query the Server

### Uniscan - WebServer Fingerprinting (Kali)

* Use `uniscan -h` for usage techniques
* `uniscan -u http://10.10.10.12:8080/CEH -qwed` -u url scan . -q directory check, - w file check, -e robots.txt and sitemap.xml check, -d for dynamic checks
* To view report, go to /usr/share/uniscan/report

{% embed url="https://www.kali.org/tools/uniscan/" %}

### **FTP Bruteforce Credentials using a Dictionary Attack**

* `nmap -p 21 <Target IP>`
* `hydra -L usernames.txt -P passwords.txt ftp://10.10.10.10`
* `hydra -L /root/Desktop/Wordlists/Usernames.txt -P /root/Desktop/Wordlists/Passwords.txt ftp://10.10.10.11`

{% embed url="https://app.gitbook.com/o/s2H3MdEB0Qp2IbE58Gxw/s/iS3hadq7jVFgSa8k5wRA/~/changes/38/practical-ethical-hacker-notes/hydra" %}
Hydra
{% endembed %}

##







