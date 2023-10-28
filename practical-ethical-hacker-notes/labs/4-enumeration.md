# 4 - Enumeration

## Mod 04 - Enumeration

* ping www.moviescope.com –f –l 1500 -> Frame size
* tracert www.moviescope.com -> Determining hop count

### **Enumerate SNMP using snmp-check**

* nmap -sU -p 161 **\<Target IP>**
* **snmp-check \<Target IP>**

### **SNMP Enumeration (161) :**

* nmap –sU –p 161 \<Target\_IP>
* nmap -sU -p 161 --script=snmp-brute \<Target\_IP>
* msfconsole
* use auxiliary/scanner/snmp/snmp\_login
* set RHOSTS and exploit
* use auxiliary/scanner/snmp/snmp\_enum
* set RHOSTS and exploit

### **NetBIOS Enumeration (139) :**&#x20;

* nbtstat –A \<Target\_IP>
* net use
* net use \10.10.10.16\e ““\user:””
* net use \10.10.10.16\e ““/user:””

#### NetBIOS Enumerator

{% embed url="https://nbtenum.sourceforge.net/" %}

### **Enum4Linux Wins Enumeration**&#x20;

Enumerating information from Windows and Samba systems.

* enum4linux -u martin -p apple -U \<Target\_IP>-> Users Enumeration
* enum4linux -u martin -p apple -o \<Target\_IP> -> OS Enumeration
* enum4linux -u martin -p apple -P \<Target\_IP>-> Password Policy Information
* enum4linux -u martin -p apple -G \<Target\_IP> -> Groups Information
* enum4linux -u martin -p apple -S \<Target\_IP> -> Share Policy Information (SMB Shares Enumeration

### **Active Directory LDAP Enumeration** : ADExplorer

### **Enumeration using Metasploit :**

* msfdb init
* service postgresql start
* msfconsole
* msf > db\_status
* nmap -Pn -sS -A -oX Test \<Target\_IP>24
* db\_import Test
* hosts -> To show all available hosts in the subnet
* db\_nmap -sS -A \<Target\_IP>-> To extract services of particular machine
* services -> to get all available services in a subnet

### **SMB Version Enumeration using MSF**

* use scanner/smb/smb\_version
* set RHOSTS 10.10.10.8-16
* set THREADS 100
* run
* hosts -> now exact os\_flavor information has been updated



### Hyena

Expand local workstation to view Users, Services, User Rights, Scheduled Jobs

{% embed url="https://www.systemtools.com/hyena/download.htm" %}

**Accessing Shared Files**

```bash
# List All Shared Resources
net view  <IP>

# Connect to Shared Resource
net use
net use \\10.10.10.1\e ""\user:""
net use \\10.10.10.1\e ""/user:""
```





#### **Addition**

* nbtstat -a **\<Target IP>** (Windows)
* nbtstat -c
