---
description: https://darkside.com.au/snow/
---

# ⛄ Snow

**SNOW** is used to conceal messages in ASCII text by appending whitespace to the end of lines. Because spaces and tabs are generally not visible in text viewers, the message is effectively hidden from casual observers. And if the built-in encryption is used, the message cannot be read even if it is detected.

> \-m is the message you want to hide
>
> \-p is the password
>
> original.txt is the original file
>
> cipher.txt is the target file

#### Windows

* snow.exe -C -p 1234 -m "Secret Message" original.txt cipher.txt

To unhide the hidden text

* snow.exe -C -p 1234 cipher.txt

#### Linux

* ./snow -C -p "magic" output.txt
* snow -C -m "Secret Text Goes Here!" -p "magic" readme.txt readme2.txt • -m → Set your message • -p → Set your password

### Additional Resources

{% embed url="https://darkside.com.au/snow/" %}

{% embed url="https://github.com/Samsar4/Ethical-Hacking-Labs/blob/master/5-System-Hacking/9-Steganography.md" %}
Hiding Data using Steganography
{% endembed %}
