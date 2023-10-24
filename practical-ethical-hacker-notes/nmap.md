---
description: https://www.kali.org/tools/nmap/ https://nmap.org/
---

# 👁 Nmap

### Introduction to Nmap

Nmap **allows you to scan your network and discover not only everything connected to it**, but also a wide variety of information about what's connected, what services each host is operating, and so on. It was created by Gordon Lyon. It supports a large number of scanning techniques, such as UDP, TCP connect (), TCP SYN (half-open), and FTP. Nmap provides a number of features for probing computer networks, including host discovery and service and operating system detection.

### Basic command

```
nmap -p- -sC -sV -O -A -T4 -oA nmapOutputfile 10.10.X.X

    • -p- -> Scans all the ports from 0 to 65535 available on the IP
    • -sC -> Runs default scripts
    • -sV -> version enumeration or service version
    • -O  -> OS enumeration
    • -A  -> Enumerate all the stuff as much as it can
    • -T4 -> fast as time 4 (default is 3)
    • -oA -> store the output on 3 types of format(nmap, gnmap, xml)
```

### Cheatsheet for nmap

This cheat sheet was prepared by [https://www.stationx.net/nmap-cheat-sheet/](https://www.stationx.net/nmap-cheat-sheet/). You can also check out the cheatsheet. I've attached the file below👇🏻

{% embed url="https://www.stationx.net/nmap-cheat-sheet/" %}
[https://www.stationx.net/nmap-cheat-sheet/](https://www.stationx.net/nmap-cheat-sheet/)
{% endembed %}

#### Switches in nmap which you might need to know

<table><thead><tr><th width="185.26939394008483" align="center">Switch</th><th width="568.4285714285713">Description</th></tr></thead><tbody><tr><td align="center">-sA</td><td>ACK scan</td></tr><tr><td align="center">-sF</td><td>FIN scan</td></tr><tr><td align="center">-sI</td><td>IDLE scan</td></tr><tr><td align="center">-sL</td><td>DNS scan (list scan)</td></tr><tr><td align="center">-sN</td><td>NULL scan</td></tr><tr><td align="center">-sO</td><td>Protocol scan (tests which IP protocols respond)</td></tr><tr><td align="center">-sP</td><td>Ping scan</td></tr><tr><td align="center">-sR</td><td>RPC scan</td></tr><tr><td align="center">-sS</td><td>SYN scan</td></tr><tr><td align="center">-sT</td><td>TCP connect scan</td></tr><tr><td align="center">-sW</td><td>Window scan</td></tr><tr><td align="center">-sX</td><td>XMAS scan</td></tr><tr><td align="center">-A</td><td>OS detection, version detection, script scanning and traceroute</td></tr><tr><td align="center">-PI</td><td>ICMP ping</td></tr><tr><td align="center">-Po</td><td>No ping</td></tr><tr><td align="center">-PS</td><td>SYN ping</td></tr><tr><td align="center">-PT</td><td>TCP ping</td></tr><tr><td align="center">-oA</td><td>output the results in 3 types of format(nmap, gnmap, xml)</td></tr><tr><td align="center">-oN</td><td>Normal output</td></tr><tr><td align="center">-oX</td><td>XML output</td></tr><tr><td align="center">-T0 through -T2</td><td>Serial scans. T0 is slowest</td></tr><tr><td align="center">-T3 through -T5</td><td>Parallel scans. T3 is slowest</td></tr><tr><td align="center">--min-rate</td><td>Minimum packet sent for second</td></tr></tbody></table>

### Port specific NSE scripts

Using NSE we can perform specific enumeration or exploitation on a host.

```
ls /usr/share/nmap/scripts/ssh*
ls /usr/share/nmap/scripts/smb*
```

We can also use nmap to discover hosts in a given IP subnet.

**Note:** In the upcoming section, you will learn what the nmap is and its uses are. Please refer to the below section.

```
nmap -sn 10.10.1.1-254 -vv -oA nmapHostsOutput
    • -sn -> Disable Port scanning
    • -vv -> verbose mode
    • -0A -> output the results in 3 types of format(nmap, gnmap, xml)
```

### Bypassing Firewall

<table><thead><tr><th width="232.33333333333331">Switch</th><th width="242.5840801265156">Example</th><th>Description</th></tr></thead><tbody><tr><td>-f</td><td>nmap -f 10.10.10.10</td><td></td></tr><tr><td>-g</td><td>nmap -g 80 10.10.10.10</td><td>Port Manipulation</td></tr><tr><td>-mtu</td><td>nmap -mtu 8 10.10.10.10</td><td>Crunching down Packets to 8 Byte</td></tr><tr><td>-D RND</td><td>nmap -D RND:10 10.10.10.10</td><td>Perform Decoy Scan and Generates Random non-reserved IP</td></tr><tr><td></td><td></td><td></td></tr><tr><td>—data 0xdeadbeef</td><td>nmap 10.10.10.10 --data 0xdeadbeef</td><td></td></tr><tr><td>Send the binary data 0's and 1's</td><td></td><td></td></tr><tr><td>--data-string "Ph34r my l33t skills"</td><td>nmap 10.10.10.10 --data-string "Ph34r my l33t skills"</td><td></td></tr><tr><td>Send strings as payload</td><td></td><td></td></tr><tr><td>--data-length 5</td><td></td><td></td></tr><tr><td>nmap --data-length 5 10.10.10.10</td><td></td><td></td></tr><tr><td>--randomize-hosts</td><td>nmap --randomize-hosts 10.10.10.10</td><td></td></tr><tr><td>send request to a IP from Random non-reserved IP</td><td></td><td></td></tr><tr><td>--badsum</td><td>nmap --badsum 10.10.10.10</td><td>Sends Bad or Bongus TCP/USP Checksum</td></tr></tbody></table>

To bypass firewall or monitoring system is suggests to use -T0 or -T1 flags.

**`-T#`** - `nmap` **Timing templates** - optimize and speed up scanning (higher is faster)

* `-T0` - _paranoid_ (possible IDS evasion, slow)
* `-T1` - _sneaky_ (possible IDS evasion, slow)
* `-T2` - _polite_ (less bandwidth and target machine resources, slow)
* `-T3` - _normal_ (default scan)
* `-T4` - _aggressive_ (reasonably fast, modern and reliable network)
* `-T5` - _insane_ (extraordinarily fast network)
* the lower the number the slower the scan

## Zenmap

Zenmap is the official <mark style="color:purple;">**Nmap Security Scanner GUI**</mark>. It is a multi-platform (Linux, Windows, Mac OS X, BSD, etc.) free and open source application which aims to make Nmap easy for beginners to use while providing advanced features for experienced Nmap users. Frequently used scans can be saved as profiles to make them easy to run repeatedly. A command creator allows interactive creation of Nmap command lines. Scan results can be saved and viewed later. Saved scan results can be compared with one another to see how they differ. The results of recent scans are stored in a searchable database.

{% embed url="https://nmap.org/zenmap" %}
Official Zenmap link
{% endembed %}

{% hint style="info" %}
* <mark style="color:red;">**I strongly recomend**</mark> you to go with [<mark style="color:purple;">**Zenmap**</mark>](nmap.md#zenmap) for the exam point of view.
* When you started your exam, the first objective you have to do is that start **Zenmap (GUI Version of Nmap)** scan on your windows machine.&#x20;
* The reason is that in <mark style="color:green;">**Parrot OS**</mark> you may find it hard to parse all the IPs because the <mark style="color:green;">**green colour**</mark> with the terminal might overwhelm you. Instead, the [<mark style="color:purple;">**Zenmap GUI**</mark>](nmap.md#zenmap) would be useful to find out the services, OS running on that IP with a cute User Interface.&#x20;
* **Trust me!💪🏻** this would be the great life-changer of your exam.&#x20;
* I know as a penetration tester working on the terminal is cool 😎 but in the heat of the moment, the browser-based VM would make you tense.
{% endhint %}

### Other Resources

{% embed url="https://nmap.org/man/pt_BR/index.htmlhttps://nmap.org/docs.html" %}

{% embed url="https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/" %}

{% embed url="https://hackertarget.com/nmap-tutorial/" %}

{% embed url="https://www.stationx.net/nmap-cheat-sheet/" %}

{% embed url="https://www.100security.com.br/netdiscover" %}

{% embed url="https://kalilinuxtutorials.com/netdiscover-scan-live-hosts-network/" %}

{% embed url="https://www.stationx.net/nmap-cheat-sheet/" %}

{% embed url="https://redteamtutorials.com/2018/10/14/nmap-cheatsheet/" %}

{% embed url="https://resources.infosecinstitute.com/nmap-cheat-sheet/#gref" %}

{% embed url="https://medium.com/@infosecsanyam/nmap-cheat-sheet-nmap-scanning-types-scanning-commands-nse-scripts-868a7bd7f692" %}

{% embed url="https://resources.infosecinstitute.com/network-discovery-tool/#gref" %}

[https://media.x-ra.de/doc/NmapCheatSheetv1.1.pdf](https://nmap.org/man/pt\_BR/index.htmlhttps://nmap.org/docs.htmlhttps://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/https://hackertarget.com/nmap-tutorial/https://www.stationx.net/nmap-cheat-sheet/https://media.x-ra.de/doc/NmapCheatSheetv1.1.pdfhttps://www.100security.com.br/netdiscoverhttps://kalilinuxtutorials.com/netdiscover-scan-live-hosts-network/https://www.youtube.com/watch?v=PS677owUk-chttps://www.stationx.net/nmap-cheat-sheet/https://redteamtutorials.com/2018/10/14/nmap-cheatsheet/https://resources.infosecinstitute.com/nmap-cheat-sheet/#grefhttps://medium.com/@infosecsanyam/nmap-cheat-sheet-nmap-scanning-types-scanning-commands-nse-scripts-868a7bd7f692https://resources.infosecinstitute.com/network-discovery-tool/#gref)

[https://www.youtube.com/watch?v=PS677owUk-c](https://nmap.org/man/pt\_BR/index.htmlhttps://nmap.org/docs.htmlhttps://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/https://hackertarget.com/nmap-tutorial/https://www.stationx.net/nmap-cheat-sheet/https://media.x-ra.de/doc/NmapCheatSheetv1.1.pdfhttps://www.100security.com.br/netdiscoverhttps://kalilinuxtutorials.com/netdiscover-scan-live-hosts-network/https://www.youtube.com/watch?v=PS677owUk-chttps://www.stationx.net/nmap-cheat-sheet/https://redteamtutorials.com/2018/10/14/nmap-cheatsheet/https://resources.infosecinstitute.com/nmap-cheat-sheet/#grefhttps://medium.com/@infosecsanyam/nmap-cheat-sheet-nmap-scanning-types-scanning-commands-nse-scripts-868a7bd7f692https://resources.infosecinstitute.com/network-discovery-tool/#gref)



