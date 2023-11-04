---
description: https://www.kali.org/tools/steghide/
---

# ⚙ Steghide

#### **Hide**

* steghide  embed  -ef  \<filename>  -cf  \<image>  -p  \<passphrase>

or

* steghide embed -cf \[img file] -ef \[file to be hide]
* steghide embed -cf 1.jpg -ef 1.txt
* Enter password or skip

#### **Extract**

* steghide info 1.jpg
* steghide extract -sf 1.jpg
* Enter password if it does exist

{% embed url="https://www.kali.org/tools/steghide/" %}

### Additional Resources

{% embed url="https://github.com/Samsar4/Ethical-Hacking-Labs/blob/master/5-System-Hacking/9-Steganography.md" %}
Hiding Data using Steganography
{% endembed %}
