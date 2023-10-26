# 2 - Footprinting & Recon

## Module 02 - Footprinting and Reconnaissance

#### v10

### Ex 1 - Open Source Information Gathering using Windows command line utilities

### Ping

```bash
ping <Target_IP> -f -l 1500 # -f switch sets the Do Not Fragment bit on the ping packet - l buffer size
```

If we receive error "packet needs to be fragmented but DF set., we can decrease -l value (buffer size).

### Tracert

Traceroutes the network configuration information on the target domain

```bash
tracert <Target_IP> 
```

### Ex 2 - Collecting information about a target website using Firebug

Firebug integrates with Firefox providing a lot of development tools to edit, debug and monitor CSS, HTML and JavaScript live in any web page.

### Ex 3 - Mirroring website using HTTrack Web Site Copier

It allows you to download a World Wide Web site from the Internet to a local directory, building recursively all directories, getting HTML, images, and other files from the server to your computer. HTTrack arranges the original site's relative link-structure. Simply open a page of the "mirrored" website in your browser, and you can browse the site from link to link, as if you were viewing it online.

Using Scan Rules tab we can add custom file format to select.

After downloading all, we can press Browse Mirrored Website to see website dumped.

### Ex 4 - Advanced network route tracing using Path Analyzer Pro

Network route tracing can determine the intermediate nodes traversed towards the destination and can detect the complete route (path) from source to destination.

Set Protocol -> ICMP

Target -> \<Target\_IP>

Port -> 65535

Time to trace -> 3 min

Stop or wait finish, and see report, synopsis log stats and others output.

### Ex 5 - Information Gathering using Metasploit

```bash
service postgresql start && msfconsole -q #start postgresql service and msfconsole
msfdb init #initialize msfdb
db_status #check if postgresql is connected to msf
db_nmap -Pn -sS -A -oX Test 10.10.10.0/24
hosts #display IP hosts
use scanner/smb/smb_version
show options #set RHOSTS, set THREADS 100
```





{% embed url="https://www.stationx.net/google-dorks-cheat-sheet/" %}
