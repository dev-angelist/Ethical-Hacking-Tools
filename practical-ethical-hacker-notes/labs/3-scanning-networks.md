# 3 - Scanning Networks

## Module 03 - Scanning Networks

<details>

<summary>EMPTY</summary>



</details>



### Perform Host Discovery

### Perform Host Discovery using Nmap









#### **Scanning entire Network**

* **nmap -Pn -sS -A -vv  \<Target\_IP>/\<Subnet> -oA \<Filename>**
  * **-Pn:** Disable ping
  * **-sS**: SYN scan
  * **-A**: Aggressive Scan
  * **-oA**: Normal\_XML and Grepable format all at once
  * **-vv**: Verbose
* **nmap -sn -PR \<Target IP>**
  * **-sn:** Disable port scan
  * **-PR:** ARP ping scan
* **nmap -sn -PU \<Target IP>**
  * **-PU:** UDP ping scan
* **nmap -sn -PE \<Target IP or IP Range>**
  * **-PE:** ICMP ECHO ping scan
* **nmap -sn -PP \<Target IP>**
  * **-PP:** ICMP timestamp ping scan
* **nmap -sn -PM \<Target IP>**
  * **-PM:** ICMP address mask ping scan
* **nmap -sn -PS \<Target IP>**
  * **-PS:** TCP SYN Ping scan
* **nmap -sn -PA \<Target IP>**
  * **-PA:** TCP ACK Ping scan
* **nmap -sn -PO \<Target IP>**
  * **-PO:** IP Protocol Ping scan

#### Convert Nmap XML file to HTML Report

xsltproc \<nmap-output.xml> -o \<nmap-output.html>

### Perform Host Discovery using Angry IP Scanner







{% embed url="https://angryip.org/download/#windows" %}

## Perform Port and Service Discovery

**Ports** are used to identify a single **network process**, to make sure the transport layer know what the destination process is.

* **`<IP>:<Port>`** pair identifies a process on a network. For example: `192.168.13.2:80`
* **1024 well-known ports** are used for the most common services: 0-1023. They are assigned by IANA in [this registry](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml).
* A **`daemon`** is a program that runs a service. Its configuration can be changed, so the service listening port can be changed in order to make recognition harder.
* Server-Client applications know which port to use because the TCP/UDP header contains two fields for the source/destination ports.

#### **Common ports**

|      Port     |        Service        |
| :-----------: | :-------------------: |
|       21      |          FTP          |
|       22      |          SSH          |
|       23      |         Telnet        |
|       25      |          SMTP         |
|       80      |          HTTP         |
|      110      |          POP3         |
| 137, 138, 139 |        NetBIOS        |
|      143      |          IMAP         |
|      443      | HTTPS (HTTP over SSL) |
|   1433-1434   |  Microsoft Sql Server |
|      3306     |         MySQL         |
|      3389     | RDP (Terminal Server) |

<div align="left">

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

</div>

> 💻 Check _listening ports_ and TCP connections on a host with the commands below:

|                                                                              Command                                                                              | Operating System |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--------------: |
| <p><strong><code>netstat -tunp</code></strong><br><strong><code>netstat -tulpn</code></strong> (listening ports too)<br><strong><code>ss -tnl</code></strong></p> |       Linux      |
|                                                                         **`netstat -ano`**                                                                        |      Windows     |
|                         <p><strong><code>netstat -p tcp -p udp</code></strong><br><strong><code>lsof -n -i4TCP -i4UDP</code></strong></p>                         | \*nix / Mac OS X |

**Linux**

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

**Windows**

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

* [TCPView](https://docs.microsoft.com/en-us/sysinternals/downloads/tcpview) tool from Microsoft Sysinternals shows detailed listings of all TCP and UDP connections.















### Perform Port and Service Discovery using MegaPing









### Explore Various Network Scanning Techniques using Nmap

* **nmap -sT -v \<Target IP>**
  * **-sT:** TCP connect/full open scan
  * **-v:** Verbose output
* **nmap -sS -v \<Target IP>**
  * **-sS:** Stealth scan/TCP hall-open scan
* **nmap -sX -v \<Target IP>**
  * **-sX:** Xmax scan
* **nmap -sM -v \<Target IP>**
  * **-sM:** TCP Maimon scan
* **nmap -sA -v \<Target IP>**
  * **-sA:** ACK flag probe scan
* **nmap -sU -v \<Target IP>**
  * **-sU:** UDP scan
* **nmap -sI -v \<Target IP>**
  * **-sI:** IDLE/IPID Header scan
* **nmap -sY -v \<Target IP>**
  * **-sY:** SCTP INIT Scan
* **nmap -sZ -v \<Target IP>**
  * **-sZ:** SCTP COOKIE ECHO Scan
* **nmap -sV -v \<Target IP>**
  * **-sV:** Detect service versions
* **nmap -A -v \<Target IP>**
  * **-A:** Aggressive scan

**Other Nmap useful flags**

* \-sN: null scan
* \-sC: enable script scanning
* \-T: enable timing options
* \-o: output options
* \-O: enable OS detection
* \--script: specifies a script
* \-f: fragment packets
* \-g or --source-port: source port manipulation
* \-mtu: Maximum Transmission Unit
* \-p: port(s) to scan
* \-D: decoy scan
* \-D RND: generates random & non-reserved IPs
* \-d: increase debugging level

### Explore Various Network Scanning Techniques using Hping3

`hping3 --scan 1-3000 -S 10.10.10.10`\
\--scan parameter defines the port range to scan and –S represents SYN flag.

Pinging the target using HPing3:\
`hping3 -c 3 10.10.10.10`\
\-c 3 means that we only want to send three packets to the target machine.

UDP Packet Crafting\
`hping3 10.10.10.10 --udp --rand-source --data 500`

TCP SYN request\
`hping3 -S 10.10.10.10 -p 80 -c 5`

\-S will perform TCP SYN request on the target machine, -p will pass the traffic through which port is assigned, and -c is the count of the packets sent to the Target machine.

HPing flood\
`hping3 10.10.10.10 --flood`

## Perform OS Discovery

### Identify the target system's OS with Time-to-Live and TCP Win size using Wireshark

Basically ping a machine from different operating systems and capture the packets from wireshark. we can check the ICMP packets, viewing the details of IPV4 packets and check the TTL \[ time to live] values.

* Open Wireshark and start capture
* Ping a target machine
* Stop capture
* Filter protocol ICMP
* Check TTL value in the Network Layer (3) details.

| Operating System | Default TTL Value (in Seconds) |
| ---------------- | ------------------------------ |
| Windows          | 128                            |
| MacOS            | 64                             |
| Linux            | 64                             |
| Android/iOS      | 64                             |
| FreeBSD          | 64                             |

### Perform OS Discovery using Nmap Script Engine (NSE)





* **nmap -A -v  \<Target IP>**
  * **-A:** Aggressive scan
* **nmap -O -v \<Target IP>**
  * **-O:** OS discovery
* **nmap –script smb-os-discovery.nse \<Target IP>**
  * **-–script:** Specify the customized script
  * **smb-os-discovery.nse:** Determine the OS, computer name, domain, workgroup, and current time over the SMB protocol (Port 445 or 139)

## Scan beyond IDS and Firewall

### Scan beyond IDS/Firewall using various Evasion Techniques



















### Ex 2 - Collecting information about a target website using Firebug

Firebug integrates with Firefox providing a lot of development tools to edit, debug and monitor CSS, HTML and JavaScript live in any web page.

###



## Perform Network Scanning using Various Scanning Tools

### Scan a target Network using Metasploit

```bash
service postgresql start && msfconsole -q #start postgresql service and msfconsole
msfdb init #initialize msfdb
db_status #check if postgresql is connected to msf
db_nmap -Pn -sS -A -oX Test 10.10.10.0/24
hosts #display IP hosts
use scanner/smb/smb_version
show options #set RHOSTS, set THREADS 100
```

### Scanning SMB Version for OS Detection using Metaspolit

```bash
use scanner/smb/smb_version
show options 
set RHOSTS 10.10.10.8-16 
set THREADS 100 
run  
hosts #Type hosts again and os_flavor will be visible
```

## Additional Resources

### Web Scanners

{% embed url="https://blog.clusterweb.com.br/?p=1297" %}

{% embed url="https://hackertarget.com/nikto-tutorial/" %}

{% embed url="https://geekflare.com/nikto-webserver-scanner/" %}

{% embed url="https://blog.sucuri.net/2015/12/using-wpscan-finding-wordpress-vulnerabilities.htmlhttps://www.hackingtutorials.org/web-application-hacking/hack-a-wordpress-website-with-wpscan/https://linuxhint.com/wpscan_wordpress_vulnerabilities_scan/" %}

{% embed url="https://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-5-creating-custom-wordlist-with-cewl-0158855/" %}

{% embed url="https://medium.com/tech-zoom/dirb-a-web-content-scanner-bc9cba624c86" %}

{% embed url="https://www.hackingarticles.in/comprehensive-guide-on-dirb-tool/" %}

#### YT videos

[https://www.youtube.com/watch?v=K78YOmbuT48](https://blog.clusterweb.com.br/?p=1297https://hackertarget.com/nikto-tutorial/https://geekflare.com/nikto-webserver-scanner/https://www.youtube.com/watch?v=K78YOmbuT48https://blog.sucuri.net/2015/12/using-wpscan-finding-wordpress-vulnerabilities.htmlhttps://www.hackingtutorials.org/web-application-hacking/hack-a-wordpress-website-with-wpscan/https://linuxhint.com/wpscan\_wordpress\_vulnerabilities\_scan/https://www.youtube.com/watch?v=SS991k5Alp0https://www.youtube.com/watch?v=MtyhOrBfG-Ehttps://www.youtube.com/watch?v=sQ4TtFdaiRAhttps://www.exploit-db.com/docs/english/45556-wordpress-penetration-testing-using-wpscan-and-metasploit.pdf?rsshttps://www.wpwhitesecurity.com/strong-wordpress-passwords-wpscan/https://www.youtube.com/watch?v=BTGP5sZfJKYhttps://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-5-creating-custom-wordlist-with-cewl-0158855/https://medium.com/tech-zoom/dirb-a-web-content-scanner-bc9cba624c86https://www.hackingarticles.in/comprehensive-guide-on-dirb-tool/)[\
\
https://www.youtube.com/watch?v=SS991k5Alp0\
\
https://www.youtube.com/watch?v=MtyhOrBfG-E\
\
https://www.youtube.com/watch?v=sQ4TtFdaiRA\
\
https://www.youtube.com/watch?v=BTGP5sZfJKY\
\
](https://blog.clusterweb.com.br/?p=1297https://hackertarget.com/nikto-tutorial/https://geekflare.com/nikto-webserver-scanner/https://www.youtube.com/watch?v=K78YOmbuT48https://blog.sucuri.net/2015/12/using-wpscan-finding-wordpress-vulnerabilities.htmlhttps://www.hackingtutorials.org/web-application-hacking/hack-a-wordpress-website-with-wpscan/https://linuxhint.com/wpscan\_wordpress\_vulnerabilities\_scan/https://www.youtube.com/watch?v=SS991k5Alp0https://www.youtube.com/watch?v=MtyhOrBfG-Ehttps://www.youtube.com/watch?v=sQ4TtFdaiRAhttps://www.exploit-db.com/docs/english/45556-wordpress-penetration-testing-using-wpscan-and-metasploit.pdf?rsshttps://www.wpwhitesecurity.com/strong-wordpress-passwords-wpscan/https://www.youtube.com/watch?v=BTGP5sZfJKYhttps://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-5-creating-custom-wordlist-with-cewl-0158855/https://medium.com/tech-zoom/dirb-a-web-content-scanner-bc9cba624c86https://www.hackingarticles.in/comprehensive-guide-on-dirb-tool/)
