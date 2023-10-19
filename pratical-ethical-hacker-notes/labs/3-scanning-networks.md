# 3 - Scanning Networks

## Module 03 - Scanning Networks

### **Lab1 - Task1: Host discovery**

* **nmap -sn -PR \[IP]**
  * **-sn:** Disable port scan
  * **-PR:** ARP ping scan
* **nmap -sn -PU \[IP]**
  * **-PU:** UDP ping scan
* **nmap -sn -PE \[IP or IP Range]**
  * **-PE:** ICMP ECHO ping scan
* **nmap -sn -PP \[IP]**
  * **-PP:** ICMP timestamp ping scan
* **nmap -sn -PM \[IP]**
  * **-PM:** ICMP address mask ping scan
* **nmap -sn -PS \[IP]**
  * **-PS:** TCP SYN Ping scan
* **nmap -sn -PA \[IP]**
  * **-PA:** TCP ACK Ping scan
* **nmap -sn -PO \[IP]**
  * **-PO:** IP Protocol Ping scan

### **Lab2 - Task3: Port and Service Discovery**

* **nmap -sT -v \[IP]**
  * **-sT:** TCP connect/full open scan
  * **-v:** Verbose output
* **nmap -sS -v \[IP]**
  * **-sS:** Stealth scan/TCP hall-open scan
* **nmap -sX -v \[IP]**
  * **-sX:** Xmax scan
* **nmap -sM -v \[IP]**
  * **-sM:** TCP Maimon scan
* **nmap -sA -v \[IP]**
  * **-sA:** ACK flag probe scan
* **nmap -sU -v \[IP]**
  * **-sU:** UDP scan
* **nmap -sI -v \[IP]**
  * **-sI:** IDLE/IPID Header scan
* **nmap -sY -v \[IP]**
  * **-sY:** SCTP INIT Scan
* **nmap -sZ -v \[IP]**
  * **-sZ:** SCTP COOKIE ECHO Scan
* **nmap -sV -v \[IP]**
  * **-sV:** Detect service versions
* **nmap -A -v \[IP]**
  * **-A:** Aggressive scan

### **Lab3 - Task2: OS Discovery**

* **nmap -A -v \[IP]**
  * **-A:** Aggressive scan
* **nmap -O -v \[IP]**
  * **-O:** OS discovery
* **nmap –script smb-os-discovery.nse \[IP]**
  * **-–script:** Specify the customized script
  * **smb-os-discovery.nse:** Determine the OS, computer name, domain, workgroup, and current time over the SMB protocol (Port 445 or 139)
