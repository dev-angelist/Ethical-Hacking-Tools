# Study Walkthrough

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
* DVWA 🏠 [THM Room](https://medium.com/techiepedia/certified-ethical-hacker-practical-exam-guide-dce1f4f216c9)[\
  ](https://tryhackme.com/room/lianyuhttps://tryhackme.com/room/startup)







* Smag Grotto 🚩 [THM CTF](https://tryhackme.com/room/smaggrotto) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/smag-grotto)
* Carnage 🚩 [THM CTF](https://tryhackme.com/room/c2carnage) 🟠 - My Writeup
* Warzone 1 🚩 [THM CTF ](https://tryhackme.com/room/warzoneone)🟠 - My Writeup
* Misguided Ghost 🚩 [THM CTF ](https://tryhackme.com/room/misguidedghosts)🔴 - My Writeup





