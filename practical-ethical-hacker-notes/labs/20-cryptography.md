# 20 - Cryptography

## **Module 20 - Cryptography**

<details>

<summary>EMPTY</summary>



</details>

####

## Creating Self-Signed Certificate with Inetmgr

* Open inetmgr
* Click machine name and select Server Certificates
* From actions select Create Self signed Certificate
* Choose Name and Personal. Go to a Site, choose Bindings from the Action panel
* Select Add
* Select Https, IP 10.10.10.16, hostname www.goodshopping.com, select the certificate
* Go the site and right click refresh one time.

## Hash identifier

* **Hash Identifier** https://www.onlinehashcrack.com/hash-identification.php
* **Hash-identifier** (CLI)
* **Hashid** (CLI)
* **sha256sum**

{% embed url="https://www.kali.org/tools/hashid/" %}

### Find/Decrypt Hash Online

* **Hashes.com**

{% embed url="https://hashes.com/en/decrypt/hash" %}

* **CrackStation.net**

{% embed url="https://crackstation.net/" %}

* **CyberChef**

{% embed url="https://gchq.github.io/CyberChef/" %}

#### Windows

### Calculate Hash of text/File by HashCalc

{% content-ref url="../hashcalc.md" %}
[hashcalc.md](../hashcalc.md)
{% endcontent-ref %}

### **Calculate MD5 Hashes using MD5 Calculator**

{% content-ref url="../md5-calculator.md" %}
[md5-calculator.md](../md5-calculator.md)
{% endcontent-ref %}

### Encode and Decode Text using BCTextEncoder

<div align="left">

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

</div>

{% content-ref url="../bctextencoder.md" %}
[bctextencoder.md](../bctextencoder.md)
{% endcontent-ref %}

### Encode/Decode Text (File Extension is .hex) using CrypTool

* File → New → Enter Text → Encrypt/Decrypt → Symmetric (Modern) → RC2 → KEY 05 → Encrypt
* File → Open → Encrypt/Decrypt → Symmetric (Modern) → RC2 → KEY 05 → Decrypt

{% embed url="https://www.cryptool.org/en/" %}

#### Linux

### Decrypt Hash using Hashcat

```bash
# In Parrot/Kali
hash-identifier #to identify the type of hash, its mode etc
hashid -m <hash> #alternative
 
hashcat -h

-a attack mode
-m hashtype
900 md4
1000 NTLM
1800 SHA512CRYPT
110 SHA1 with SALT HASH
0  MD5
100 SHA1
1400 SHA256
3200 BCRYPT
160 HMAC-SHA1
        
 #Decrypt Hashes
 hashcat '5f4dcc3b5aa765d61d8327deb882cf99' /usr/share/wordlists/rockyou.txt
 hashcat -a 3 -m 900 hash.txt /usr/share/wordlists/rockyou.txt
```

{% content-ref url="../hashcat.md" %}
[hashcat.md](../hashcat.md)
{% endcontent-ref %}

### **Decrypt Hash using John the Ripper**

* First analyze hash type -> `john hashfile.hash`
* Then crack hash -> `john hashfile.hash --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-SHA1`
* Show the cracked password -> `john --show --format=Raw-SHA1 hashfile.hash` OR \`john --show hashfile.hash

{% content-ref url="../john-the-ripper.md" %}
[john-the-ripper.md](../john-the-ripper.md)
{% endcontent-ref %}

### **Perform Disk Encryption using VeraCrypt**

Create Encrypted containers which can be mounted as Virtual Disks.

#### Creation

* Click VeraCrypt
* Create Volumn
* Create an encrypted file container
* Specify a path and file name
* Set password
* Select NAT
* Move the mouse randomly for some seconds, and click Format
* Exit

#### Mount Volume

* Select a drive, select file, open, mount
* Input password
* Dismount
* Exit

{% embed url="https://www.veracrypt.fr/en/Beginner's%20Tutorial.html" %}
VeraCrypt Step by step tutorial
{% endembed %}

{% content-ref url="../veracrypt.md" %}
[veracrypt.md](../veracrypt.md)
{% endcontent-ref %}

## Check if file is modified

We can do this comparing file hashes.

#### Windows

* **Get-FileHash** is the built-in PowerShell cmdlet that can be used to generate a hash value, allowing you to verify against the reference hash.

```bash
Get-FileHash <Location> -A SHA256 (SHA-1/256/384/512/MD5)
(Get-FileHash <Location> -A SHA256 ).hash -eq "<hash value>" #will return true or false
```

{% embed url="https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.3" %}

* **WinMD5Free:** A simple and free utility that allows you to calculate and compare MD5 checksums in Windows. You can drag and drop files into the program to generate and compare checksums.
* **FCIV (Microsoft File Checksum Integrity Verifier):** A command-line utility provided by Microsoft that allows you to compute and verify hash values for files. You can use it to create checksums and compare them.
* **HashMyFiles:** A free utility from NirSoft that provides a graphical user interface for calculating and comparing file hashes. It allows you to compare the hashes of multiple files at once.
* **File Checksum Tool:** A user-friendly tool that can calculate and compare checksums for various hash algorithms like MD5, SHA-1, and SHA-256. It provides an easy way to verify file integrity.

#### Linux

* **sha256sum (or md5sum, sha1sum):** These are built-in Linux commands for calculating the hash (SHA-256, MD5, SHA-1) of a file. You can use them in the terminal to calculate and compare checksums.
* **GtkHash:** A graphical tool for Linux that supports various hash algorithms and provides a user-friendly interface for calculating and comparing file hashes. It integrates well with the Linux desktop environment.
* **RapidCRC:** While primarily designed for Windows, there is a Linux version available. It's a user-friendly tool that supports a variety of checksum algorithms and is particularly useful for comparing and verifying large sets of files.
* **Hashdeep:** A command-line tool for hashing files in Linux and Windows. It can create hash sets for multiple files and directories, and it's useful for verifying file integrity.
