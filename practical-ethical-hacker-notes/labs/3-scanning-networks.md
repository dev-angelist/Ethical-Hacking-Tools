# 3 - Scanning Networks

## Module 03 - Scanning Networks

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

### Explore Various Network Scanning Techniques using Hping3





\
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
