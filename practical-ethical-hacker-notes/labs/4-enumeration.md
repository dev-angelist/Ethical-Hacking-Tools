# 4 - Enumeration

## Mod 04 - Enumeration

#### Basic command

* ping www.moviescope.com –f –l 1500 -> Frame size
* tracert www.moviescope.com -> Determining hop count

### Ping Sweep

Ping Sweep is a network scanning technique used to determine which IP addresses in a range are active or responsive. It involves sending Internet Control Message Protocol (ICMP) echo requests (ping) to a range of IP addresses and then analyzing the responses. When a target IP address responds to the ping request, it indicates that a host is active and reachable.

#### Nmap

* nmap -sP \<Target\_IP>/\<Subnet>

#### Bash

We can se the 'ping' command on a given subnet range to check host statuses. The goal is to produce a clean output, focusing solely on the IP addresses, by filtering out unnecessary information.

* ping -c 3 \<Target\_IP>

Grabbing only IP addresses:

```bash
# -c number of packets sent, grep to consider only strings with 64 bytes, cut to remove whitespaces,
#tr to remove ":" symbol and > to export the results to a .txt file 
ping -c 3 <Target_IP> | grep "64" | cut -d " " -f 4 | tr -d ":" ; > iptest.txt
```

We can automate it creating a bash script (.sh):

#### pingsweep.sh

```bash
#!/bin/bash 
 
if [ "$1" == "" ]
then
echo "[-] You forgot the IP address!"
echo "[-] Syntax: ./ipsweep.sh 10.10.10"

else
for ip in `seq 1 254`; do 
ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" &
done
fi
```

Save it, change the permissions and make executable:

```bash
chmod 770 pingweep.sh
chmod +x pingweep.sh

#Test it out
./pingweep.sh 10.0.2 > ping-results.txt
cat ping-results.txt
```

### **SNMP Enumeration (161)**&#x20;

SNMP enumeration is the process of enumerating the users accounts and devices on a SNMP enabled computer.

SNMP service comes with two passwords, which are used to configure and access the SNMP agent from the management station. They are: Read community string and Read/Write community string. These strings (passwords) come with a default value, which is same for all the systems. They become easy entry points for attackers if left unchanged by administrator.

```bash
nmap –sU –p 161 <Target_IP> #-sU: UDP port scan
nmap -sU -p 161 --script=snmp-brute <Target_IP>
msfconsole #run msfconsole
use auxiliary/scanner/snmp/snmp_login
set RHOSTS and exploit
use auxiliary/scanner/snmp/snmp_enum
set RHOSTS and exploit
```

### **Enumerate SNMP using snmp-check**

* nmap -sU -p 161 \<Target IP>
* snmp-check \<Target IP>

### **NetBIOS Enumeration (139) :**&#x20;

* nbtstat –A \<Target\_IP>
* net use
* net use \10.10.10.16\e ““\user:””
* net use \10.10.10.16\e ““/user:””

#### NetBIOS Enumerator

{% embed url="https://nbtenum.sourceforge.net/" %}

### **Enum4Linux Wins Enumeration**&#x20;

Enum4linux is a tool for gathering information from Windows and Samba systems. Security professionals use it to identify vulnerabilities and potential attack vectors. During assessments, they establish connections with the target system to discover weaknesses and enhance system security.

* enum4linux -u martin -p apple -U \<Target\_IP> -> Users Enumeration
* enum4linux -u martin -p apple -o \<Target\_IP> -> OS Enumeration
* enum4linux -u martin -p apple -P \<Target\_IP> -> Password Policy Information
* enum4linux -u martin -p apple -G \<Target\_IP> -> Groups Information
* enum4linux -u martin -p apple -S \<Target\_IP> -> Share Policy Information (SMB Shares Enumeration

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

## **Active Directory LDAP Enumeration**

### ADExplorer

Active Directory Explorer (AD Explorer) is a robust tool for viewing and editing Active Directory (AD). With it, you can effortlessly navigate the AD database, bookmark preferred locations, inspect object properties and attributes without opening dialog boxes, modify permissions, examine an object's schema, and perform complex, saveable searches.

{% embed url="https://docs.microsoft.com/en-us/sysinternals/downloads/adexplorer" %}

### Hyena

Hyena offers comprehensive Active Directory (AD) reporting, featuring built-in tools for customizable queries, filtering, object property management, advanced attribute handling, and numerous other AD administration capabilities.

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
