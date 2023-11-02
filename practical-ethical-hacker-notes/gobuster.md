---
description: https://www.kali.org/tools/gobuster/ https://github.com/OJ/gobuster
---

# 🔗 Gobuster

* `gobuster -e -u` [`http://10.10.10.10`](http://192.168.0.155/) `-w wordlist.txt`
* `gobuster dir -u 10.10.162.67 -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt`
* `gobuster dir -u http://<TARGET_IP> -w /usr/share/wordlists/dirb/common.txt -b 403,404`
* `gobuster dir -u http://<TARGET_IP> -w /usr/share/wordlists/dirb/common.txt -b 403,404 -x .php,.xml,.txt -r`
* `gobuster dir -u http://<TARGET_IP>/data -w /usr/share/wordlists/dirb/common.txt -b 403,404 -x .php,.xml,.txt -r`

## **Alternative tool**

### Ffuf

#### Directory discovery:

ffuf -w wordlist.txt -u http://example.com/FUZZ

#### File discovery:

ffuf -w wordlist.txt -u http://example.com/FUZZ -e .aspx,.php,.txt,.html

#### Output of responses with status code:

ffuf -w /usr/share/wordlists/dirb/small.txt -u http://example.com/FUZZ -mc 200,301

#### The -maxtime flag offers to end the ongoing fuzzing after the specified time in seconds:

ffuf -w wordlist.txt -u http://example.com/FUZZ -maxtime 60

#### Number of threads:

ffuf -w wordlist.txt -u http://example.com/FUZZ -t 64

### **Dirbuster**

* `dirb` [`http://`](http://192.168.1.224/)`10.10.10.10 wordlist.txt`
