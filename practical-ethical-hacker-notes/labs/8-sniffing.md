# 8 - Sniffing

## Module 08 - Sniffing

<details>

<summary>What is Sniffing?</summary>

Sniffing can be used to capture a variety of types of traffic, including:

* **HTTP traffic:** This includes traffic from web browsers and servers. HTTP traffic is often not encrypted, so it can be easily captured and analyzed.
* **Email traffic:** This includes traffic from email servers and clients. Email traffic is often encrypted, but there are vulnerabilities that can be exploited to decrypt it.
* **IM traffic:** This includes traffic from instant messaging applications. IM traffic is often not encrypted, so it can be easily captured and analyzed.
* **File transfer traffic:** This includes traffic from file transfer applications, such as FTP and SCP. File transfer traffic is often not encrypted, so it can be easily captured and analyzed.

Sniffing can be used for a variety of ethical hacking purposes, including:

* **Identifying vulnerabilities in networks and systems:** Sniffing can be used to identify vulnerabilities in networks and systems by looking for patterns in traffic. For example, an ethical hacker might sniff traffic for cleartext passwords or sensitive data.
* **Gathering intelligence on attackers:** Sniffing can be used to gather intelligence on attackers by monitoring their traffic. For example, an ethical hacker might sniff traffic for IP addresses or domains that are associated with known attackers.
* **Testing security measures:** Sniffing can be used to test the effectiveness of security measures, such as firewalls and intrusion detection systems. For example, an ethical hacker might sniff traffic to see if it is being properly filtered by a firewall.
* Sniffing can be done using a variety of tools, both free and commercial. Some popular sniffing tools include Wireshark and TCPdump.
* Sniffing can be done on both wired and wireless networks.
* Sniffing can be detected by some security measures, such as intrusion detection systems. However, there are ways to evade detection.
* It is important to note that sniffing is illegal in many jurisdictions without the permission of the network owner.

**Protocols which are affected**

Protocols such as the tried and true TCP/IP were never designed with security in mind and therefore do not offer much resistance to potential intruders. Several rules lend themselves to easy sniffing.

* **HTTP** − It is used to send information in the clear text without any encryption and thus a real target.
* **SMTP** _(Simple Mail Transfer Protocol)_ − SMTP is basically utilized in the transfer of emails. This protocol is efficient, but it does not include any protection against sniffing.
* **NNTP** \_(Network News Transfer Protocol)\_− It is used for all types of communications, but its main drawback is that data and even passwords are sent over the network as clear text.
* **POP** _(Post Office Protocol)_ − POP is strictly used to receive emails from the servers. This protocol does not include protection against sniffing because it can be trapped.
* **FTP** _(File Transfer Protocol)_ − FTP is used to send and receive files, but it does not offer any security features. All the data is sent as clear text that can be easily sniffed.
* **IMAP** _(Internet Message Access Protocol)_ − IMAP is same as SMTP in its functions, but it is highly vulnerable to sniffing.
* **Telnet** − Telnet sends everything (usernames, passwords, keystrokes) over the network as clear text and hence, it can be easily sniffed.

</details>



* `http.request.method == “POST”` -> Wireshark filter for filtering HTTP POST request&#x20;
* Capture traffic from remote interface via wireshark
  * Capture > Options > Manage Interfaces&#x20;
  * Remote Interface > Add > Host &  Port (2002)
  * Username & password > Start

### **Lab2 - Task1: Password Sniffing using Wireshark**

#### **Attacker**

* Wireshark

#### **Target**

* [www.moviescope.com](http://www.moviescope.com/)
* Login

#### **Attacker**

* Stop capture
* File-\&gt;Save as
* Filter: **http.request.method==POST**
* RDP log in Target
* service
* start Remote Packet Capture Protocol v.0 (experimental)
* Log off Target
* Wireshark-\&gt;Capture options-\&gt;Manage Interface-\&gt;Remote Interfaces
* Add a remote host and its interface
* Fill info

#### **Target**

* Log in
* Browse website and log in

#### **Attacker**

* Get packets

### Detect ARP Poisoning using Wireshark

* Create an attack between two machines as shown above.
* Here, Attacker is 10.10.10.10. Victims are 10.10.10.11 and 10.10.10.16.
* Generate some random traffic between the victims e.g from .11 machine use: `hping3 -c 100000 10.10.10.16`
* Open Wireshark on Attacker machine.
* Click Edit -> Preferences -> Protocols -> ARP/RARP -> **Detect ARP** request storms and Detect duplicate IP address configuration -> Start Capture.
* Analyze -> Expert Information

{% content-ref url="../wireshark-or-tcpdump.md" %}
[wireshark-or-tcpdump.md](../wireshark-or-tcpdump.md)
{% endcontent-ref %}

### Cain & Abel – MITM attack tool (via ARP Poisoning)&#x20;

* Click **Configure**.
* Select Adapter with the Attacker’s IP in the Sniffer tab.
* Click on **Start/Stop Sniffer** (2nd icon in icon list) icon.
* Go to the **Sniffer** Sub tab.
* Click the **Blue + (Add)** icon.
* In MAC Scanner window select **All Hosts** and **All Tests**.
* Click **ARP** on lower left corner. Then click anywhere inside ARP window to so + icon is clickable.
* Select 1st victim IP (10.10.10.10), now select 2nd victim IP (10.10.10.12). Click on **Start/Stop ARP** (3rd icon in icon list) icon.
* Now do FTP from .12 IP to .10 with credentials martin:apple.
* Observe that packets will be generated in cain.
* Click **Passwords** -> **FTP** -> View captured credentials.

### MITM attack using BetterCAP <a href="#user-content-mitm-attack-using-bettercap" id="user-content-mitm-attack-using-bettercap"></a>

{% embed url="https://github.com/Samsar4/Ethical-Hacking-Labs/blob/master/7-Sniffing/1-MITM-with-Bettercap.md" %}

## MAC Address Spoofing

**MAC spoofing** is a technique for changing a factory-assigned Media Access Control (MAC) address of a network interface on a networked device. The MAC address that is hard-coded on a network interface controller (NIC) cannot be changed. However, many drivers allow the MAC address to be changed. Additionally, there are tools which can make an operating system believe that the NIC has the MAC address of a user's choosing. The process of masking a MAC address is known as MAC spoofing. Essentially, MAC spoofing entails changing a computer's identity, for any reason, and it is relatively easy.

#### Why changing MAC address?

* Increase anonymity.
* Impersonate other devices.
* Bypass filters.

#### Requisites <a href="#user-content-requisites" id="user-content-requisites"></a>

* Kali Linux virtual machine.
* Alfa network adapter, or other with similar chipset. [\[+\]](https://kennyvn.com/best-wireless-adapters-kali-linux/)
* Windows 7, 8 or 10 virtual machine.

#### Linux

### Using Macchanger <a href="#user-content-using-macchanger-kali" id="user-content-using-macchanger-kali"></a>

Macchanger is a tool that is included with any version of Kali Linux rolling edition and can change the MAC address to any desired address until the next reboot. In this lab we will be spoofing the MAC address of our wireless adapter with a random MAC address generated by **Macchanger on Kali Linux.**

Repo: [https://github.com/alobbs/macchanger](https://github.com/alobbs/macchanger)

1. Use `ifconfig` to see your current MAC address of your Network adapter:\
   \
   `ifconfig`
2. Turn off the Network adapter:\
   \
   `ifconfig wlan1 down`
3. Next, change your MAC address to a new random MAC Address using `macchanger`:\
   \
   `macchanger -r wlan1`

```
Current MAC:   f2:30:a0:1a:44:b3 (unknown)
Permanent MAC: 00:c1:c8:a1:e7:d9 (ALFA, INC.)
New MAC:       ce:11:9a:98:fp:ad (unknown)
```

{% embed url="https://www.kali.org/tools/macchanger/" %}

### Changing MAC address manually <a href="#user-content-changing-mac-address-manually-kali" id="user-content-changing-mac-address-manually-kali"></a>

1. Turn off the Network adapter:\
   \
   `ifconfig wlan0 down`
2. Change the address using `hw ether` option from **ifconfig** using any MAC address you want:\
   \
   `ifconfig wlan0 hw ether 00:11:22:33:44:55`
3. Enable the interface:\
   \
   `ifconfig wlan0 up`
4. Check the changes of the network adapter:\
   \
   `ifconfig`

#### Windows

### SMAC GUI Tool

SMAC is a powerful and easy-to-use tool for MAC address changer (spoofer). The tool can activate a new MAC address right after changing it automatically.

[https://smac.soft32.com/](https://smac.soft32.com/)\


<figure><img src="https://camo.githubusercontent.com/38719274db7bdfc3e0efc1304ac39ed773f795f784d2b619cdb615ab9f94cacd/68747470733a2f2f7468656765656b706167652e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031362f30352f6d61632d616464726573732d6368616e6765722d746f6f6c2e676966" alt=""><figcaption></figcaption></figure>

## Additional Resources

{% embed url="https://www.varonis.com/blog/how-to-use-wireshark/" %}

{% embed url="https://hackertarget.com/wireshark-tutorial-and-cheat-sheet/" %}

{% embed url="https://www.lifewire.com/wireshark-tutorial-4143298" %}

{% embed url="https://www.comparitech.com/net-admin/wireshark-cheat-sheet/" %}

{% embed url="https://medium.com/hacker-toolbelt/wireshark-filters-cheat-sheet-eacdc438969c" %}

{% embed url="https://github.com/security-cheatsheet/wireshark-cheatsheet" %}

{% embed url="https://www.cellstream.com/resources/2013-09-10-11-55-21/cellstream-public-documents/wireshark-related/83-wireshark-display-filter-cheat-sheet/file" %}

{% embed url="https://www.howtogeek.com/104278/how-to-use-wireshark-to-capture-filter-and-inspect-packets/" %}

{% embed url="https://www.guru99.com/wireshark-passwords-sniffer.html" %}

{% embed url="https://danielmiessler.com/study/tcpdump/" %}

{% embed url="https://hackertarget.com/tcpdump-examples/" %}

{% embed url="https://opensource.com/article/18/10/introduction-tcpdump" %}

[https://www.youtube.com/watch?v=4\_7A8Ikp5Cc](https://www.youtube.com/watch?v=TkCSr30UojMhttps://www.varonis.com/blog/how-to-use-wireshark/https://hackertarget.com/wireshark-tutorial-and-cheat-sheet/https://www.lifewire.com/wireshark-tutorial-4143298https://www.comparitech.com/net-admin/wireshark-cheat-sheet/https://medium.com/hacker-toolbelt/wireshark-filters-cheat-sheet-eacdc438969chttps://github.com/security-cheatsheet/wireshark-cheatsheethttps://www.cellstream.com/resources/2013-09-10-11-55-21/cellstream-public-documents/wireshark-related/83-wireshark-display-filter-cheat-sheet/filehttps://www.howtogeek.com/104278/how-to-use-wireshark-to-capture-filter-and-inspect-packets/https://www.youtube.com/watch?v=4\_7A8Ikp5Cchttps://www.guru99.com/wireshark-passwords-sniffer.htmlhttps://danielmiessler.com/study/tcpdump/https://hackertarget.com/tcpdump-examples/https://opensource.com/article/18/10/introduction-tcpdump)

[https://www.youtube.com/watch?v=TkCSr30UojM](https://www.youtube.com/watch?v=TkCSr30UojM)
