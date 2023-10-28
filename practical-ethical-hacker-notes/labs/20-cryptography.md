# 20 - Cryptography

## **Module 20 - Cryptography**

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
