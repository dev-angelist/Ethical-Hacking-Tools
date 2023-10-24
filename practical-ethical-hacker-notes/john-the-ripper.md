---
description: https://www.kali.org/tools/john/
---

# 🥷 John the Ripper

Windows

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

Linux

```
at /etc/shadow

# Metasploit
use post/linux/gather/hashdump

john --format=sha512crypt linux.hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt
john -wordlist /usr/share/wordlists/rockyou.txt crack.hash
john -wordlist /usr/share/wordlists/rockyou.txt -users users.txt test.hash
```

### Other References:

* [Password Cracking With John The Ripper - RAR/ZIP & Linux Passwords](https://www.youtube.com/watch?v=XjVYl1Ts6XI) - HackerSploit
