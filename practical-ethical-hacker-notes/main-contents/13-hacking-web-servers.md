# 13 - Hacking Web Servers

#### <mark style="color:red;">**Module 13 - Hacking Web Servers**</mark>

<details>

<summary>What is a Web Server?</summary>

A **web server** is a software or hardware system that serves as the backbone of the World Wide Web, delivering web content to users' web browsers. It handles client requests for web pages, processes those requests, and sends back the requested web content, which may include HTML pages, images, scripts, stylesheets, and other files. Web servers are an essential component of the internet and play a central role in the process of serving websites and web applications to users.

Here are some key characteristics and functions of web servers:

1. **Request-Response Model**: Web servers operate on a request-response model. They receive incoming HTTP (Hypertext Transfer Protocol) requests from web browsers, process those requests, and send back HTTP responses containing the requested web content.
2. **Content Storage**: Web servers store web content and files, which are organized in a directory structure. These files can be static (unchanging) or dynamic (generated on-the-fly based on user input or data from databases).
3. **HTTP Handling**: Web servers are designed to understand and interpret the HTTP protocol, which is used for communication between web clients (typically web browsers) and the server. They handle various HTTP methods like GET, POST, PUT, DELETE, and more.
4. **Security**: Web servers often include security features to protect against common web threats, such as Distributed Denial of Service (DDoS) attacks, and they can be configured to support secure communication using HTTPS (HTTP Secure) with SSL/TLS encryption.
5. **Server-Side Scripting**: Many web servers support server-side scripting languages like PHP, Python, Ruby, and Node.js. These scripts allow dynamic generation of web content, database interactions, and more.
6. **Logging and Monitoring**: Web servers typically generate logs that record incoming requests, server responses, and errors. These logs can be valuable for troubleshooting and security analysis.
7. **Load Balancing**: In high-traffic scenarios, multiple web servers may be used in a load-balancing setup to distribute incoming requests and ensure optimal performance and availability.
8. **Caching**: Web servers often include caching mechanisms to store and serve frequently requested resources more quickly, reducing server load and improving response times.
9. **Reverse Proxy**: In some configurations, web servers can act as reverse proxies, sitting in front of application servers and forwarding client requests to the appropriate backend systems.

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

{% content-ref url="../tools/hydra.md" %}
[hydra.md](../tools/hydra.md)
{% endcontent-ref %}

### **Useful default password list**

* [http://www.phenoelit.org/dpl/dpl.html](http://www.phenoelit.org/dpl/dpl.html)
* [https://datarecovery.com/rd/default-passwords/](https://datarecovery.com/rd/default-passwords/)
* [https://github.com/Dormidera/WordList-Compendium](https://github.com/Dormidera/WordList-Compendium)

### **Making custom wordlist from website keywords:**

* **`cewl`**` ``example.com -m 5 -w words.txt`

where **cewl** is the tool, **example.com** is the site, **-m** is to specify the minimum length of the word , **-w** is to specify the output file

{% content-ref url="../tools/cewl.md" %}
[cewl.md](../tools/cewl.md)
{% endcontent-ref %}
