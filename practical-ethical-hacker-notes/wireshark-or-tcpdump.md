---
description: https://www.kali.org/tools/wireshark/ https://www.kali.org/tools/tcpdump/
---

# 🦈 Wireshark or Tcpdump

## Wireshark

```bash
wireshark -i eth1

# Filter by ip
ip.add == 10.10.10.9

# Filter by dest ip
ip.dest == 10.10.10.15

# Filter by source ip
ip.src == 10.10.16.33

# Filter by tcp port
tcp.port == 25

# Filter by ip addr and port
ip.addr == 10.10.14.22 and tcp.port == 8080

# Filter SYN flag
tcp.flags.syn == 1 and tcp.flags.ack ==0

# Broadcast filter
eth.dst == ff:ff:ff:ff:ff:ff
```

### Filters CheatSheet

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### TShark

```bash
tshark -D
tshark -i eth1
tshark -r <FILE>.pcap
tshark -r <FILE>.pcap | wc -l

# First 100 packets
tshark -r <FILE>.pcap -c 100

# Protocl hierarchy statistics
tshark -r <FILE>.pcap -z io,phs -q

# HTTP traffic
tshark -r <FILE>.pcap -Y 'http' | more
tshark -r <FILE>.pcap -Y "ip.src==<SOURCE_IP> && ip.dst==<DEST_IP>"

# Only GET requests
tshark -r <FILE>.pcap -Y "http.request.method==GET"

# Packets with frame time, source IP and URL for all GET requests
tshark -r <FILE>.pcap -Y "http.request.method==GET" -Tfields -e frame.time -e ip.src -e http.request.full_uri

# Packets with a string
tshark -r <FILE>.pcap -Y "http contains password"

# Check destination IP
tshark -r <FILE>.pcap -Y "http.request.method==GET && http.host==<TARGET_URL>" -Tfields -e ip.dst

# Check session ID
tshark -r <FILE>.pcap -Y "ip contains amazon.in && ip.src==<IP>" -Tfields -e ip.src -e http.cookie

# Check OS/User Agent type
tshark -r <FILE>.pcap -Y "ip.src==<IP> && http" -Tfields -e http.user_agent

# WiFi traffic filter
tshark -r <FILE>.pcap -Y "wlan"

# Only deauthentication packets 
tshark -r <FILE>.pcap -Y "wlan.fc.type_subtype==0x000c"
# and devices
tshark -r <FILE>.pcap -Y "wlan.fc.type_subtype==0x000c" -Tfields -e wlan.ra

# Only WPA handshake packets
tshark -r <FILE>.pcap -Y "eapol"

# Onyl SSID/BSSID
tshark -r <FILE>.pcap -Y "wlan.fc.type_subtype==8" -Tfields -e wlan.ssid -e wlan.bssid

tshark -r <FILE>.pcap -Y "wlan.ssid==<SSID>" -Tfields -e wlan.bssid

# WiFi Channel
tshark -r <FILE>.pcap -Y "wlan.ssid==<SSID>" -Tfields -e wlan_radio.channel

# Vendor & model
tshark -r <FILE>.pcap -Y "wlan.ta==<DEVICE_MAC> && http" -Tfields -e http.user_agent
```

```bash
# ARP POISONING - arpspoof

## Forward IP packets
echo 1 > /proc/sys/net/ipv4/ip_forward
# arpspoof -i <interface> -t <target> -r <host>
arpspoof -i eth1 -t <TARGET_IP> -r <HOST_IP>
```

#### Others Notes

```bash
#To find DOS (SYN and ACK)
tcp.flags.syn == 1  , tcp.flags.syn == 1 and tcp.flags.ack == 0

#To find passwords
http.request.method == POST

#More reference
https://www.comparitech.com/net-admin/wireshark-cheat-sheet/

#To find DOS: look for Red and Black packets with around 1-2 simple packets in between and then pick any packet and check the Source and Destination IP with port(As per question)
#To find DOS (SYN and ACK) : tcp.flags.syn == 1  , tcp.flags.syn == 1 and tcp.flags.ack == 0
#To find passwords : http.request.method == POST
```

## **Password sniffing using Wireshark** <a href="#734c" id="734c"></a>

**Attacker**

* Stop capture
* File-\&gt;Save as
* Filter: http.request.method==POST
* RDP log in Target
* service
* start Remote Packet Capture Protocol v.0 (experimental)
* Log off Target
* Wireshark-\&gt;Capture options-\&gt;Manage Interface-\&gt;Remote Interfaces
* Add a remote host and its interface
* Fill info

### Additional Resources

{% embed url="https://github.com/Samsar4/Ethical-Hacking-Labs/blob/master/11-Bonus/TCPDump-Tutorial.md" %}
TCPDUMP Tutorial
{% endembed %}

{% embed url="https://github.com/Samsar4/Ethical-Hacking-Labs/blob/master/9-Denial-of-Service/3-Detecting-DoS-Traffic.md" %}
Detecting DoS Attack traffic
{% endembed %}

{% embed url="https://www.varonis.com/blog/how-to-use-wireshark/" %}

{% embed url="https://hackertarget.com/wireshark-tutorial-and-cheat-sheet/" %}

{% embed url="https://www.lifewire.com/wireshark-tutorial-4143298" %}

{% embed url="https://www.comparitech.com/net-admin/wireshark-cheat-sheet/" %}

{% embed url="https://medium.com/hacker-toolbelt/wireshark-filters-cheat-sheet-eacdc438969chttps://github.com/security-cheatsheet/wireshark-cheatsheet" %}

{% embed url="https://www.howtogeek.com/104278/how-to-use-wireshark-to-capture-filter-and-inspect-packets/" %}

{% embed url="https://www.guru99.com/wireshark-passwords-sniffer.html" %}

{% embed url="https://danielmiessler.com/study/tcpdump/" %}

{% embed url="https://hackertarget.com/tcpdump-examples/" %}

{% embed url="https://opensource.com/article/18/10/introduction-tcpdump" %}

[https://www.youtube.com/watch?v=4\_7A8Ikp5Cc](https://www.varonis.com/blog/how-to-use-wireshark/https://hackertarget.com/wireshark-tutorial-and-cheat-sheet/https://www.lifewire.com/wireshark-tutorial-4143298https://www.comparitech.com/net-admin/wireshark-cheat-sheet/https://medium.com/hacker-toolbelt/wireshark-filters-cheat-sheet-eacdc438969chttps://github.com/security-cheatsheet/wireshark-cheatsheethttps://www.cellstream.com/resources/2013-09-10-11-55-21/cellstream-public-documents/wireshark-related/83-wireshark-display-filter-cheat-sheet/filehttps://www.howtogeek.com/104278/how-to-use-wireshark-to-capture-filter-and-inspect-packets/https://www.youtube.com/watch?v=4\_7A8Ikp5Cchttps://www.guru99.com/wireshark-passwords-sniffer.htmlhttps://danielmiessler.com/study/tcpdump/https://hackertarget.com/tcpdump-examples/https://opensource.com/article/18/10/introduction-tcpdump)
