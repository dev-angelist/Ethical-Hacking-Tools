---
description: https://www.kali.org/tools/hashcat/
---

# 😺 Hashcat

### Windows

```
hashcat -a 3 -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt
hashcat -a 3 -m 1000 --show hashes.txt /usr/share/wordlists/rockyou.txt
hashcat -m 1000 -a 0 -o found.txt --remove crack.hash rockyou-10.txt
```

### Linux

```
hashcat --help | grep 1800
hashcat -a 3 -m 1800 linux.hashes.txt /usr/share/wordlists/rockyou.txt
ashcat -m 1000 -a 0 -o found.txt --remove crack.hash rockyou-10.txt
```

### Dictionary Attack

<pre class="language-bash"><code class="lang-bash"><strong>hashcat -m 0 -a 0 -o cracked.txt target_hashes.txt /usr/share/wordlists/rockyou.txt
</strong>  -m 0 designates the type of hash we are cracking (MD5);
  -a 0 designates a dictionary attack;
  -o cracked.txt is the output file for the cracked passwords;
  -target_hashes.txt is our input file of hashes;
  -/usr/share/wordlists/rockyou.txt = Path to the wordlist
 
 m - 0:MD5
     100:SHA1
     1400:SHA256
     1700:SHA512
     900:MD4
     3200:BCRYPT
</code></pre>

#### Also Important to check hash

```
#hash-identifier
#hash -m [file]
```

### Other References:

* [Password cracking with Kali Linux and HashCat](https://www.youtube.com/watch?v=z4\_oqTZJqCo) - NetworkChuck

\
