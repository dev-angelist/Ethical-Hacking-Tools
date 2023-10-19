# 8 - Sniffing

## Module 08 - Sniffing

* `http.request.method == “POST”` -> Wireshark filter for filtering HTTP POST request&#x20;
* Capture traffic from remote interface via wireshark
  * Capture > Options > Manage Interfaces&#x20;
  * Remote Interface > Add > Host &  Port (2002)
  * Username & password > Start

### **Lab2 - Task1: Password Sniffing using Wireshark**

* **Attacker**
  * Wireshark
* **Target**
  * [www.moviescope.com](http://www.moviescope.com/)
  * Login
* **Attacker**
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
* **Target**
  * Log in
  * Browse website and log in
* **Attacker**
  * Get packets
