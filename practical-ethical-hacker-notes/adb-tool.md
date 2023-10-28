# 🤖 Adb tool

```bash
apt-get update
sudo apt-get install adb -y
adb devices -l

# Connection Establish Steps
adb connect 192.168.0.4:5555
adb devices -l
adb shell  

# Download a File from Android using ADB tool
adb pull /sdcard/log.txt C:\Users\admin\Desktop\log.txt 
adb pull sdcard/log.txt /home/mmurphy/Desktop
```

* via USB
* ./adb tcpip 5555
* ./adb connect 192.168.43.117:5555
* ./adb devices
* ./adb  -d shell (Direct an adb command to the only attached USB device)
* cd sdcard
* cd dcim
* cd camera
* ./adb   push C:\platform-tools\\[ota.zip](http://ota.zip/) &#x20;
* /sdcard/Download -> from pc to android)
* pc location -> \<android location>
* ./adb
* pull  /sdcard/Download/magisk\_patched.img&#x20;
* C:\platform-tools -> from android to pc
* android location -> \<pc location>







### Connect to Android through ADB and access files via shell

[https://www.youtube.com/watch?v=Hvreb4hjsig](https://www.youtube.com/watch?v=Hvreb4hjsig)
