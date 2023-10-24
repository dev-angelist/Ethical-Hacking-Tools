---
description: https://www.kali.org/tools/hashcat/
---

# 😺 Hashcat

Windows

```
hashcat -a 3 -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt
hashcat -a 3 -m 1000 --show hashes.txt /usr/share/wordlists/rockyou.txt
hashcat -m 1000 -a 0 -o found.txt --remove crack.hash rockyou-10.txt
```

Linux

```
hashcat --help | grep 1800
hashcat -a 3 -m 1800 linux.hashes.txt /usr/share/wordlists/rockyou.txt
ashcat -m 1000 -a 0 -o found.txt --remove crack.hash rockyou-10.txt
```

### Other References:

* [Password cracking with Kali Linux and HashCat](https://www.youtube.com/watch?v=z4\_oqTZJqCo) - NetworkChuck

\
