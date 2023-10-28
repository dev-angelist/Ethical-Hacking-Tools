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









### Connect to Android through ADB and access files via shell

[https://www.youtube.com/watch?v=Hvreb4hjsig](https://www.youtube.com/watch?v=Hvreb4hjsig)
