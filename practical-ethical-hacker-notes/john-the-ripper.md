---
description: https://www.kali.org/tools/john/
---

# 🥷 John the Ripper

### Windows

```
john --list=formats | grep NT
john --format=NT hashes.txt

gzip -d /usr/share/wordlists/rockyou.txt.gz
john <Hash_Password-File> --wordlist=/usr/share/wordlists/rockyou.txt # To crack the password from your previous output (hashdump,shadow file )
john --format=NT win_hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt

john -wordlist /usr/share/wordlists/rockyou.txt crack.hash
john -wordlist /usr/share/wordlists/rockyou.txt -users users.txt test.hash

#this is another way to crack passwords (that requires shadow file with passwd file)
unshadow passwd shadow > unshadowed.txt
john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
```

### Linux

```
at /etc/shadow

# Metasploit
use post/linux/gather/hashdump

john --format=sha512crypt linux.hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt
john -wordlist /usr/share/wordlists/rockyou.txt crack.hash
john -wordlist /usr/share/wordlists/rockyou.txt -users users.txt test.hash
```



<pre class="language-bash"><code class="lang-bash">#Single crack mode
john --single --format=raw-sha1 crack.txt

#Crack the password in file using wordlist
john --wordlist=/usr/share/john/password.lst --format=raw-sha1 crack.txt (Crack.txt here contains the hashes)

#Cracking service credentials like SSH
1. First have to convert the hash file to JOHN format : ssh2john /home/text/.ssh/id_rsa > crack.txt (Now we need to crack this crack.txt file with John The Ripper)
2. john --wordlist=/usr/share/wordlists/rockyou.txt crack.txt

#To crack ZIP
1. zip2john file.zip > crack.txt
2. john --wordlist=/usr/share/wordlists/rockyou.txt crack.txt

<strong>#Notes:
</strong>–wordlist can be written as -w also
john crack.txt --wordlist=rockyou.txt --format=Raw-SHA256
</code></pre>



### Other References:



[Password Cracking With John The Ripper - RAR/ZIP & Linux Passwords](https://www.youtube.com/watch?v=XjVYl1Ts6XI) - Video Tutorial

{% embed url="https://linuxconfig.org/password-cracking-with-john-the-ripper-on-linux" %}

{% embed url="https://medium.com/@sc015020/how-to-crack-passwords-with-john-the-ripper-fdb98449ff1" %}

{% embed url="https://www.varonis.com/blog/john-the-ripper/" %}







