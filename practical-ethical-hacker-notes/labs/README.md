# 🧪 Labs

abs Walkthrough 🔭

* [2 - Footprinting & Reconnaissance](2-footprinting-and-recon.md)
* [3 - Scanning Networks](3-scanning-networks.md)
* [4 - Enumeration](4-enumeration.md)
* [5 - Vulnerability Analysis](5-vulnerability-analysis.md)
* [6 - System Hacking](6-system-hacking.md)
* [8 - Sniffing](8-sniffing.md)
* [10 - DoS](10-dos.md)
* [13 - Hacking Web Servers](13-hacking-web-servers.md)
* [14 - Hacking Web Applications](14-hacking-web-apps.md)
* [15 - SQL Injection](15-sql-injection.md)
* [17 - Hacking Mobile Platform](17-hacking-mobile.md)
* [19 - Cloud Computing](19-cloud-computing.md)
* [20 - Cryptography](20-cryptography.md)







<details>

<summary>Covert</summary>

Covert\_tcp [source code](https://github.com/infovault-Ytube/CEH-Practical-Notes/blob/main/covert\_tcp.c) Live Demo [Covert TCP Live Demo-Youtube](https://www.youtube.com/watch?v=bDcz4qIpiQ4)

```
# Compile the Code  
cc -o covert_tcp covert_tcp.c
  
# Reciever Machine(192.168.29.53)  
sudo ./covert_tcp -dest 192.168.29.53 -source 192.168.29.123 -source_port 9999 -dest_port 8888 -server -file recieve.txt  
 
# Sender Machine(192.168.29.123) 
# Create A Message file that need to be transferred Eg:secret.txt
sudo ./covert_tcp -dest 192.168.29.53 -source 192.168.29.123 -source_port 8888 -dest_port 9999 -file secret.txt
```

[Wireshark Capture](https://github.com/infovault-Ytube/CEH-Practical-Notes/blob/main/Covert\_TCP-Capture.pcapng) Hello This 123 -



</details>

<figure><img src="https://github.com/infovault-Ytube/CEH-Practical-Notes/raw/main/covertCapture.jpg" alt=""><figcaption></figcaption></figure>

