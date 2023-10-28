# 8 - Sniffing

## Module 08 - Sniffing

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
