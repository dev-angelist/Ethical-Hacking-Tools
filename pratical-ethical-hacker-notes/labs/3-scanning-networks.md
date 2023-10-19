# 3 - Scanning Networks

## Module 03 - Scanning Networks

### **Lab1 - Task1: Host discovery**

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

### **Lab2 - Task3: Port and Service Discovery**

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

### **Lab3 - Task2: OS Discovery**

* **nmap -A -v  \<Target IP>**
  * **-A:** Aggressive scan
* **nmap -O -v \<Target IP>**
  * **-O:** OS discovery
* **nmap –script smb-os-discovery.nse \<Target IP>**
  * **-–script:** Specify the customized script
  * **smb-os-discovery.nse:** Determine the OS, computer name, domain, workgroup, and current time over the SMB protocol (Port 445 or 139)
