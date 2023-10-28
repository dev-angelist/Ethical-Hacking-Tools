# Study Walkthrough

If you have money, you can afford iLabs because the challenges are based on the iLab environment and you will get hands-on practice to clear this exam.

If you can’t afford iLab, there are many platforms in which you can practice the listed tools. I personally prefer TryHackMe and HackTheBox. This Exam is all about how much knowledge you have on tools.







**Windows based Commands which will help you to find the answers.**\
**1)** **net user** — For Domain Users Enumeration\
**2)** **snow.exe** -C -p “password” stegfile.txt\
**3)** **type** C:\path.txt — It displays the content of the path.txt file.\
**4)** **dir**\
**5)** **cd**\
**6)** **hostname**\
**7)** **whoami**\
**8)** **PWd**



## Linux <a href="#effd" id="effd"></a>

**Linux based tools**\
1\) Nmap\
2\) wpscan\
3\) sqlmap\
4\) hashcat\
5\) john\
6\) Hydra\
7\) PhoneSploit\
8\) Metasploit



### Commands were used during the exam <a href="#7129" id="7129"></a>

**8) Metasploit**\
If you get any questions related to netbios, SMB use metasploit.





**All the commands that you need to know:**

How many machines are active in a network - net discover -i 192.168.1.0/24

Connect to RDP via cmd - mstsc&#x20;

* **Find DNS records -** [https://www.nslookup.io/](https://www.nslookup.io/)

Scan the whole website- (skipfish -o /root/test -S /usr/share/skipfish/dictionaries/complete.wl [http://10.10.10.10:8080](http://10.10.10.10:8080/))

\-o output

\-S wordlist&#x20;

* **To brute force directories or files-**

robuster dir  -u 10.10.10.10  -w /usr/share/dirb/wordlists/common.txt  -x  .txt

&#x20;                           OR

uniscan -u [http://10.10.10.12:8080/CEH](http://10.10.10.12:8080/CEH) -q   (for directories)

uniscan –u [http://10.10.10.12:8080/CEH](http://10.10.10.12:8080/CEH) -we (enable file check like robots.txt and sitemap.xml)

* **To get the file from the server-** get [http://10.10.10.10/secret.txt](http://10.10.10.10/secret.txt)&#x20;
* **FTP Login -** ftp \<ip>

get \<file name>   (to get file from FTP login)

**SSH Login** - SSH username@10.10.10.10

&#x20;

* **Android Hacking-**



&#x20;&#x20;

* **sqlmap-**

site:[http://testphp.vulnweb.com/](http://testphp.vulnweb.com/) php?= (for finding vulnerable site)

(for cookies- console->document.cookie)

&#x20;

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  --dbs   (databases)

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart –tables   (tables)

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart -T users --columns   (columns)

(dump whole table)

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart -T users  --dump  &#x20;

&#x20;                                                           OR                                                                                   &#x20;

(dump individual  column data)

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart -T users -C uname  --dump &#x20;

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart -T users -C pass  --dump

&#x20;

### Domande - tools

1 ) Nmap

nmap -sn 10.10.10.10/24 -ON nmap.txt&#x20;

2\) Snow

Stegnography snow.exe -C -p -password" stegfile.txt&#x20;

3\) Open Stego or Quick Stege

3\) Wpscan

wpscan -u james -P \[passwordftxt — url http://172.16.0.27:8080/CEH/&#x20;

4\) WireShark

I have perfomed DDos to practice Download from here : https://drive.google.com/drive/folders/10YvNHem8NgjLJCy1XvdYqU5cDJKlo To find DOS (SYN and ACK) : tcpflagssyn - 1 , tcp.flags.syn 1 and tcp.flags.ack 0 To find passwords : http.request.method POST&#x20;

5\) SqlMap

sqlmap -u "http://vmw.moviescope.com/viewprofile.aspx?id=l" —dbs \[ Copy the cookie from website, mysql -U qdpmadmin -h 192.168.1.8 -P passwod \[ If you have logins credentioals I&#x20;

6\) OWASP ZAP

&#x20;7\) Hashcat

hashcat -m 0 -a 0 hash.txt passwordlist.txt -m 0: MD5 hash mode -a 0: Dictionary attack mode hash.txt txt file containing hash in a compliant format passwordlist.txt: dictionary file containing passwords in plain text

&#x20;8\) John

john —format-raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt&#x20;

9\) Hydra

hydra -L /user.txt -P (password.txt ftp://172.0.16.21&#x20;

10\) Veracrypt&#x20;

11\) Crypttool&#x20;

12\) Hash Calculator&#x20;

13\) MD5 Calculator&#x20;

14\) PhoneSploit&#x20;

15\) MetaSploit

If you get any questions related to netbios, SMB use metasploit.

16\) BCTextEncoder



Tools Used da Technology Hacks (video):

**in Parrot Box:**

netdiscover, nmap, hydra, john the ripper, wpscan, sqlmap, ADB

**In Windows Box:**

Wireshark, Hashcalc, Veracrypt, BCTextEncoder, Cryptool, Snow, OpenStego

**Others exam questions:**

* How many machines are active? Use netdiscover
* Which machine has FTP Server open? Use nmap
* Find 2 secret files using FTP? brute force FTP username and psw.
* Find out phone number of Web application user? Use sqlmap
* Brute force Wordpress  website user's psw? Use wpscan
* Decode .hex file? Use Cryptool
* Which machine started DOS attack? DDOS attack happened on which IP? Find out http crediantls from PCAP file? Use wireshark
* Decode the given text using given secret? Use BCTextEncorder
* Calculate SHA1 hash of a text? Use Hashcalc
* Decrypt the hidden vulume and find secret file? Use Veracrypt.
* Crack the given hash? Use hashes.com
* Find secret hidden int he image/file? Usen openstego/snow
* Find a secret file in Android? Use ADB
* Send data to another machine (firewall blocked)? Use Covert TCP.



### My Initial way of approaching Exam/ Vuln CTF Boxes: <a href="#fed1" id="fed1"></a>

1. **netdiscover -i eth0** — This will help me to get the machines available on our network. \[ **eth0 may differ if VPN network I will be tun0** ]
2. Once I get the IP’s I will run my **Nmap** on all those IP’s.
3. **nmap -p- 10.10.10.10 \[ Any IP ]**

Once I ran the above command I will get all the opened port on that target and then with that open port, I will run another nmap, for example, if port 443,80,53,135,8080,8888 are opened then my nmap command will be.

4\. **nmap -p443,80,53,135,8080,8888 -A -O -sV -sC -T4 -oN nmapOutput 10.10.10.10**

This will find out the OS version, service version, and ran default nmap script and store the output. Storing output is very important, you may need to refer it many times.

5\. While nmap is running I will open all the IPs on browser and will see whether any web service is running on not, if Yes then I will run gobuster or dirb.

**gobuster -e -u** [**http://10.10.10.10**](http://192.168.0.155/) **-w wordlsit.txt**

**dirb** [**http://**](http://192.168.1.224/)**10.10.10.10 wordlist.txt**

6\. If I find any login page I will try SQLi manually

```
admin' --
admin' #
admin'/*
' or 1=1--
' or 1=1#
' or 1=1/*
') or '1'='1--
') or ('1'='1—
```

7\. Brute Forcing services !! and making custom wordlists is always an added advantage but make sure the service won’t be down OR lock you out from trying again.

**Some of the default password list:**

* [http://www.phenoelit.org/dpl/dpl.html](http://www.phenoelit.org/dpl/dpl.html)
* [https://datarecovery.com/rd/default-passwords/](https://datarecovery.com/rd/default-passwords/)
* [https://github.com/Dormidera/WordList-Compendium](https://github.com/Dormidera/WordList-Compendium)

**Making custom wordlist from website keywords:**

* **cewl** example.com -m 5 -w words.txt

where **cewl** is the tool, **example.com** is the site, **-m** is to specify the minimum length of the word , **-w** is to specify the output file

**Some of the service brute force with hydra:**

* hydra -l root -P passwords.txt \[-t 32] \<IP> _**ftp**_
* hydra -L usernames.txt -P pass.txt \<IP> _**mysql**_
* hydra -l USERNAME -P /path/to/passwords.txt -f \<IP> _**pop3**_ -V
* hydra -V -f -L \<userslist> -P \<passwlist> _**rdp**_://\<IP>
* hydra -P common-snmp-community-strings.txt target.com _**snmp**_
* hydra -l Administrator -P words.txt 192.168.1.12 _**smb**_ -t 1
* hydra -l root -P passwords.txt \<IP> _**ssh**_

**Searchsploit useful commands:**

* searchsploit “Linux Kernel”
* searchsploit -m 7618 — **Paste the exploit in the current directory**
* searchsploit -p 7618\[.c] — **Show complete path**
* searchsploit — nmap file.xml — **Search vulns inside a Nmap XML result**

### Some resource links will help you in the exam. <a href="#fa6c" id="fa6c"></a>

[https://github.com/cmuppin/CEH](https://github.com/cmuppin/CEH)\
[https://chirag-singla.notion.site/CEH-Practical-Preparation-7f2b77651cd144e8872f2f5a30155052](https://chirag-singla.notion.site/CEH-Practical-Preparation-7f2b77651cd144e8872f2f5a30155052)\
[https://github.com/Samsar4/Ethical-Hacking-Labs](https://github.com/Samsar4/Ethical-Hacking-Labs)\
[https://github.com/Rezkmike/CEH\_Practical\_Preparation](https://github.com/Rezkmike/CEH\_Practical\_Preparation)\
[https://www.youtube.com/watch?v=ycZFk-GT5-I](https://www.youtube.com/watch?v=ycZFk-GT5-I) (i-lab videos).

### Tips <a href="#91e1" id="91e1"></a>

_1) First finish linux based questions like nmap etc and save those in the desktop folder, believe me you will look into the nmap scans over and over again._\
_2) Watch the ilab videos from youtube and reffer CEH practical Lab manual._\
_3) Everything will be asked from the ilab videos nothing will be out of sylabus._\
_4) Be Cool._

The Username and Password file will be present in the parrot machine it will help you to crack the ftp and wordpress related questions.

Don’t be nervous, you are going to pass the exam with no doubt. Patience is really needed for the exam because the parrot machine is outdated and its very slow.



**Exam Experience:**

I know this is the most awaited part. The exam is watched over by a person called a proctor. They use GoToMeeting, a program that sees and hears you through your computer. They'll also record what's on your screen during the whole exam. After your identity is verified, your exam starts.

The exam is on a website called iLab. You don't need to worry about taking pictures of your virtual machines (VMs).

You'll get two Operating systems to test things on. One is Parrot OS, and the other is Windows 7. No more Kali this time.&#x20;

**You can DO** use the internet for the exam. You can look things up, take notes on your computer, watch videos, and read blogs. **But DON”T** write notes by hand, talk to people, or make calls.

Your exam computers won't have regular internet access. You need to use your web browser to access the internet.

* Start with the scanning part (NMAP Scan), since the scanning part takes some time, I moved on to other hacking questions.
* Scan all ports on IPs because default scripts might not catch smart configurations.





THM Materials



* Windows Fundamentals Module 🏠 [THM Room](https://tryhackme.com/module/windows-fundamentals)
* Linux Fundamentals Module 🏠 [THM Room](https://tryhackme.com/module/linux-fundamentals)
* BurpSuite: The Basics 🏠 [THM Room](https://tryhackme.com/room/burpsuitebasics)
* BurpSuite: Repeater 🏠 [THM Room](https://tryhackme.com/room/burpsuiterepeater)
* Hydra 🏠 [THM Room](https://tryhackme.com/room/hydra)
* Nmap 🏠 [THM Room](https://tryhackme.com/room/rpnmap)
* Nmap Live Host Discovery 🏠 [THM Room](https://tryhackme.com/room/nmap01)
* Crack The Hash 🏠 [THM Room](https://tryhackme.com/room/crackthehash)
* Metasploit: Introduction 🏠 [THM Room](https://tryhackme.com/room/metasploitintro)
* Metasploit 🏠 [THM Room ](https://tryhackme.com/room/metasploitintro)
* More Detailed Tutorial of Metasploit 🗒️ [NoobLinux Article](https://nooblinux.com/metasploit-tutorial/)
* SQL Injection 🏠 [THM Room](https://tryhackme.com/room/sqlilab)
* Nessus 🏠 [THM Room](https://tryhackme.com/room/rpnessusredux)
* WireShark The Basics 🏠 [THM Room](https://tryhackme.com/room/wiresharkthebasics)
* CCStego 🏠 [THM Room](https://tryhackme.com/room/ccstego)
* Tmux 🏠 [THM Room](https://tryhackme.com/room/rptmux)&#x20;
* TShark 🏠 [THM Room](https://tryhackme.com/room/tshark)
* Brooklyn Nine Nine 🚩 [THM CTF](https://tryhackme.com/room/brooklynninenine) 🟢 - My Writeup
* Lianyu 🚩 [THM CTF ](https://tryhackme.com/room/lianyu)🟢 - My Writeup
* StartUp 🚩 [THM CTF](https://tryhackme.com/room/startup) 🟢 - My Writeup
* Ice  🚩 [THM CTF ](https://tryhackme.com/room/ice)🟢 - My Writeup
* DVWA 🏠 [THM Room](https://medium.com/techiepedia/certified-ethical-hacker-practical-exam-guide-dce1f4f216c9)
* Anthem 🏠 [THM Room](https://tryhackme.com/room/anthem)
*
* Agent Sudo  🚩 [THM CTF](https://tryhackme.com/room/agentsudoctf) 🟢 - My Writeup
* Simple CTF 🚩 [THM CTF](https://tryhackme.com/room/easyctf) 🟢 - My Writeup
* AttackerKB 🚩 [THM CTF ](https://tryhackme.com/room/attackerkb)🟢 - My Writeup
* Blue  🚩 THM CTF 🟢 - My Writeup
* Ice  🚩 THM CTF 🟢 - My Writeup
* Ice  🚩 THM CTF 🟢 - My Writeup
* recommended[https://tryhackme.com/room/ccpentesting](https://tryhackme.com/room/ccpentesting)  !!! –&#x20;
* recommended[https://tryhackme.com/room/zthweb2](https://tryhackme.com/room/zthweb2)&#x20;
*
*
* [\
  ](https://tryhackme.com/room/lianyuhttps://tryhackme.com/room/startup)
*

    TRYHACKME ROADMAP⛔️⛔️

    ## Level 1 - Intro

    * [ ] OpenVPN https://tryhackme.com/room/openvpn
    * [ ] Welcome https://tryhackme.com/jr/welcome
    * [ ] Intro to Researching https://tryhackme.com/room/introtoresearch
    * [ ] Learn Linux https://tryhackme.com/room/zthlinux
    * [ ] Crash Course Pentesting https://tryhackme.com/room/ccpentesting

    Introductory CTFs to get your feet wet

    * [ ] Google Dorking https://tryhackme.com/room/googledorking
    * [ ] OHsint https://tryhackme.com/room/ohsint
    * [ ] Shodan.io https://tryhackme.com/room/shodan

    ## Level 2 - Tooling

    * [ ] Tmux https://tryhackme.com/room/rptmux
    * [ ] Nmap https://tryhackme.com/room/rpnmap
    * [ ] Web Scanning https://tryhackme.com/room/rpwebscanning
    * [ ] Sublist3r https://tryhackme.com/room/rpsublist3r
    * [ ] Metasploit https://tryhackme.com/room/rpmetasploit
    * [ ] Hydra https://tryhackme.com/room/hydra
    * [ ] Linux Privesc https://tryhackme.com/room/linuxprivesc
    * [ ] Web Scanning https://tryhackme.com/room/rpwebscanning

    More introductory CTFs

    * [ ] Vulnversity - https://tryhackme.com/room/vulnversity
    * [ ] Blue - https://tryhackme.com/room/blue
    * [ ] Simple CTF https://tryhackme.com/room/easyctf
    * [ ] Bounty Hacker https://tryhackme.com/room/cowboyhacker

    ## Level 3 - Crypto & Hashes with CTF practice

    * [ ] Crack the hash https://tryhackme.com/room/crackthehash
    * [ ] Agent Sudo https://tryhackme.com/room/agentsudoctf
    * [ ] The Cod Caper https://tryhackme.com/room/thecodcaper
    * [ ] Ice https://tryhackme.com/room/ice
    * [ ] Lazy Admin https://tryhackme.com/room/lazyadmin
    * [ ] Basic Pentesting https://tryhackme.com/room/basicpentestingjt

    ## Level 4 - Web

    * [ ] OWASP top 10 https://tryhackme.com/room/owasptop10
    * [ ] Inclusion https://tryhackme.com/room/inclusion
    * [ ] Injection https://tryhackme.com/room/injection
    * [ ] Vulnversity https://tryhackme.com/room/vulnversity
    * [ ] Basic Pentesting https://tryhackme.com/room/basicpentestingjt
    * [ ] Juiceshop https://tryhackme.com/room/owaspjuiceshop
    * [ ] Ignite https://tryhackme.com/room/ignite
    * [ ] Overpass https://tryhackme.com/room/overpass
    * [ ] Year of the Rabbit https://tryhackme.com/room/yearoftherabbit
    * [ ] DevelPy https://tryhackme.com/room/bsidesgtdevelpy
    * [ ] Jack of all trades https://tryhackme.com/room/jackofalltrades
    * [ ] Bolt https://tryhackme.com/room/bolt

    ## Level 5 - Reverse Engineering

    * [ ] Intro to x86 64 https://tryhackme.com/room/introtox8664
    * [ ] CC Ghidra https://tryhackme.com/room/ccghidra
    * [ ] CC Radare2 https://tryhackme.com/room/ccradare2
    * [ ] CC Steganography https://tryhackme.com/room/ccstego
    * [ ] Reverse Engineering https://tryhackme.com/room/reverseengineering
    * [ ] Reversing ELF https://tryhackme.com/room/reverselfiles
    * [ ] Dumping Router Firmware https://tryhackme.com/room/rfirmware

    ## Level 6 - PrivEsc

    * [ ] Sudo Security Bypass https://tryhackme.com/room/sudovulnsbypass
    * [ ] Sudo Buffer Overflow https://tryhackme.com/room/sudovulnsbof
    * [ ] Windows Privesc Arena https://tryhackme.com/room/windowsprivescarena
    * [ ] Linux Privesc Arena https://tryhackme.com/room/linuxprivescarena
    * [ ] Windows Privesc https://tryhackme.com/room/windows10privesc
    * [ ] Blaster https://tryhackme.com/room/blaster
    * [ ] Ignite https://tryhackme.com/room/ignite
    * [ ] Kenobi https://tryhackme.com/room/kenobi
    * [ ] Capture the flag https://tryhackme.com/room/c4ptur3th3fl4g
    * [ ] Pickle Rick https://tryhackme.com/room/picklerick

    ## Level 7 - CTF practice

    * [ ] Post Exploitation Basics https://tryhackme.com/room/postexploit
    * [ ] Smag Grotto https://tryhackme.com/room/smaggrotto
    * [ ] Inclusion https://tryhackme.com/room/inclusion
    * [ ] Dogcat https://tryhackme.com/room/dogcat
    * [ ] LFI basics https://tryhackme.com/room/lfibasics
    * [ ] Buffer Overflow Prep https://tryhackme.com/room/bufferoverflowprep
    * [ ] Overpass https://tryhackme.com/room/overpass
    * [ ] Break out the cage https://tryhackme.com/room/breakoutthecage1
    * [ ] Lian Yu https://tryhackme.com/room/lianyu











**Damn Vulnerable Web Application (DVWA)**

DVWA is a PHP/MYSQL vulnerable website that's made to be easy to hack. It's used to practice common web problems. It has different levels of difficulty. DVWA is important for the CEH (Practical) exam. It's a good idea to practice on DVWA because the exam might have similar challenges.

You can refer to the link [https://bughacking.com/dvwa-ultimate-guide-first-steps-and-walkthrough/](https://bughacking.com/dvwa-ultimate-guide-first-steps-and-walkthrough/) for a full guide on the setup and use of DVWA.

* **Hack The Box** (Challenges Steganography and Web) ([https://www.hackthebox.eu/](https://www.hackthebox.eu/))
* **Vulnhub** (Machines Easy to Medium) ([https://www.vulnhub.com/](https://www.vulnhub.com/))

**TryHackMe (**[**https://tryhackme.com/**](https://tryhackme.com/)**)**&#x20;





* Smag Grotto 🚩 [THM CTF](https://tryhackme.com/room/smaggrotto) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/smag-grotto)
* Carnage 🚩 [THM CTF](https://tryhackme.com/room/c2carnage) 🟠 - My Writeup
* Warzone 1 🚩 [THM CTF ](https://tryhackme.com/room/warzoneone)🟠 - My Writeup
* Misguided Ghost 🚩 [THM CTF ](https://tryhackme.com/room/misguidedghosts)🔴 - My Writeup









