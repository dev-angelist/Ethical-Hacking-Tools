---
description: https://www.kali.org/tools/wireshark/ https://www.kali.org/tools/tcpdump/
---

# 🦈 Wireshark or Tcpdump

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

