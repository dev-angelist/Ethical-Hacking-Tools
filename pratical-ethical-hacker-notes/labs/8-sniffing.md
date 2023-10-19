# 8 - Sniffing

## Module 08 - Sniffing

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
