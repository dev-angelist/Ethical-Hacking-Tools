---
description: >-
  https://www.exploit-db.com/searchsploit
  https://www.kali.org/tools/exploitdb/#searchsploit
---

# 🕷 Searchsploit

## What is SearchSploit?

SearchSploit is a command-line search tool for Exploit-DB that allows you to take a copy of the Exploit Database with you. Searchsploit is included in the Exploit Database repository on GitHub. SearchSploit is very useful for security assessments when you don’t have Internet access because it gives you the power to perform detailed offline searches for exploits in the saved Exploit-DB.

## How to install

To run SearchSploit in Kali Linux, open the terminal and type “searchsploit” to run SearchSploit as “exploitdb” package is already included in Kali Linux. However, if you are using the Kali Light variant or your custom-build ISO then you can install SearchSploit manually using the below-mentioned command.

```bash
sudo apt update && sudo apt -y install exploitdb
```

### **Updating SearchSploit**

In order to update SearchSploit, run the following command:

```bash
searchsploit -u
```

## Cheatsheet

```
========
 Options 
=========
## Search Terms
   -c, --case     [term]      Perform a case-sensitive search (Default is inSEnsITiVe)
   -e, --exact    [term]      Perform an EXACT & order match on exploit title (Default is an AND match on each term) [Implies "-t"]
                                e.g. "WordPress 4.1" would not be detect "WordPress Core 4.1")
   -s, --strict               Perform a strict search, so input values must exist, disabling fuzzy search for version range
                                e.g. "1.1" would not be detected in "1.0 < 1.3")
   -t, --title    [term]      Search JUST the exploit title (Default is title AND the file's path)
       --exclude="term"       Remove values from results. By using "|" to separate, you can chain multiple values
                                e.g. --exclude="term1|term2|term3"
       --cve      [CVE]       Search for Common Vulnerabilities and Exposures (CVE) value

## Output
   -j, --json     [term]      Show result in JSON format
   -o, --overflow [term]      Exploit titles are allowed to overflow their columns
   -p, --path     [EDB-ID]    Show the full path to an exploit (and also copies the path to the clipboard if possible)
   -v, --verbose              Display more information in output
   -w, --www      [term]      Show URLs to Exploit-DB.com rather than the local path
       --id                   Display the EDB-ID value rather than local path
       --disable-colour       Disable colour highlighting in search results

## Non-Searching
   -m, --mirror   [EDB-ID]    Mirror (aka copies) an exploit to the current working directory
   -x, --examine  [EDB-ID]    Examine (aka opens) the exploit using $PAGER

## Non-Searching
   -h, --help                 Show this help screen
   -u, --update               Check for and install any exploitdb package updates (brew, deb & git)

## Automation
       --nmap     [file.xml]  Checks all results in Nmap's XML output with service version
                                e.g.: nmap [host] -sV -oX file.xml

=======
 Notes 
=======
 * You can use any number of search terms
 * By default, search terms are not case-sensitive, ordering is irrelevant, and will search between version ranges
   * Use '-c' if you wish to reduce results by case-sensitive searching
   * And/Or '-e' if you wish to filter results by using an exact match
   * And/Or '-s' if you wish to look for an exact version match
 * Use '-t' to exclude the file's path to filter the search results
   * Remove false positives (especially when searching using numbers - i.e. versions)
 * When using '--nmap', adding '-v' (verbose), it will search for even more combinations
 * When updating or displaying help, search terms will be ignored
```

## Example of usage

```bash
==========
 Examples 
==========
  searchsploit afd windows local
  searchsploit -t oracle windows
  searchsploit -p 39446
  searchsploit linux kernel 3.2 --exclude="(PoC)|/dos/"
  searchsploit -s Apache Struts 2.0.0
  searchsploit linux reverse password
  searchsploit -j 55555 | jq
  searchsploit --cve 2021-44228

  For more examples, see the manual: https://www.exploit-db.com/searchsploit

=========
```

### **Basic Search**

You can add any number of search terms you wish to look for. In the below image, we are searching for exploits containing the term “oracle” and “windows”.

```
searchsploit windows oracle
```

<figure><img src="../.gitbook/assets/Schermata del 2023-07-09 18-56-00.png" alt=""><figcaption><p>basic search in searchsploit</p></figcaption></figure>

### **Title Searching in SearchSploit**

If you are performing Basic Search, searchsploit will check for both the path and the title of the exploit. Searches can be restricted to the titles by using the -t option as follows:

```bash
searchsploit -t windows oracle
```

<figure><img src="../.gitbook/assets/Schermata del 2023-07-09 18-57-54.png" alt=""><figcaption><p>Title Searching in SearchSploit</p></figcaption></figure>

In the above search, we are looking for the exploits related to Oracle based on Windows OS.&#x20;

### **Copying Exploit to Clipboard and Directory**

If you want to copy the exploit to clipboard use ‘-p’. For example – ” searchsploit -p XYZ ” , here XYZ is the exploit ID. If you want to copy the exploit in your current working directory use ‘-m’. For example – ” searchsploit -m XYZ “, where XYZ is the exploit ID.

```bash
searchsploit -m 44553
```

<figure><img src="../.gitbook/assets/Schermata del 2023-07-09 18-59-02.png" alt=""><figcaption><p>Copying Exploit to Clipboard and Directory</p></figcaption></figure>

### **Examine an Exploit**

If you want to examine an exploit or want to study an exploit, use ‘–examine’. For example – “searchsploit XYZ –examine” , where XYZ is the exploit ID.

```bash
searchsploit 44553 -examine
```

<figure><img src="../.gitbook/assets/Schermata del 2023-07-09 19-05-16.png" alt=""><figcaption><p>Examine an Exploit</p></figcaption></figure>

### **Eliminate Unwanted Results**

If you want to eliminate unwanted results from your search simply use ‘–exclude’. You can also remove multiple terms by separating the terms with a “|” (pipe). For example – searchsploit –exclude “PoC”.
