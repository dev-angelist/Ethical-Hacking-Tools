# 2 - Footprinting & Recon

#### <mark style="color:blue;">**Module 02 - Footprinting and Reconnaissance**</mark>

<details>

<summary>What are Footprinting and Reconnaissance?</summary>

**Footprinting** and **Reconnaissance** are two essential phases in the field of cybersecurity and information gathering that are typically conducted by ethical hackers, security professionals, or threat actors to gather information about a target organization or system. These activities are crucial for understanding the target's vulnerabilities and potential attack vectors.

**Footprinting**: Footprinting is the initial phase of the information-gathering process. It involves collecting data and information about a target system or organization, often using passive techniques that don't involve direct interaction with the target. The goal of footprinting is to create a comprehensive profile of the target, including its network structure, infrastructure, domain names, IP addresses, employee names, email addresses, and more. This information can be obtained from public sources, such as websites, social media, and public records. Footprinting techniques can include:

* DNS (Domain Name System) enumeration: Gathering information about domain names and their associated IP addresses.
* WHOIS lookups: Identifying the owner and contact information for a domain.
* Search engine queries: Using search engines to find information about the target.
* Social engineering: Gaining information through interactions with individuals associated with the target organization.
* Network scanning: Identifying open ports and services running on the target's network.

**Reconnaissance**: Reconnaissance is the second phase of information gathering and can be considered an extension of footprinting. During reconnaissance, more active techniques may be used to gather additional information about the target. The primary purpose of reconnaissance is to discover vulnerabilities and potential entry points for an attack. Reconnaissance techniques can include:

* Port scanning: Identifying open ports, services, and vulnerabilities.
* Network mapping: Creating a map of the target's network infrastructure.
* Vulnerability scanning: Identifying known security weaknesses in systems and software.
* Banner grabbing: Collecting information from banners or headers of services running on the target systems.
* Social engineering: Using psychological manipulation to extract information from individuals within the target organization.
* Active enumeration: Actively probing the target's systems and network for more detailed information.

</details>

## Perform Footprinting through Search Engines

{% embed url="https://www.stationx.net/google-dorks-cheat-sheet/" %}

## Perform Footprinting through Web Services

### Find the Company's Domains and Sub-domains using Netfcraft

Go to https://www.netcraft.com and insert company's domain.

After that you can use a people search service as https://www.peekyou.com to find people from the target organization.

In addition there're famous tools such as:

theHarvester: this tool gathers email, subdomains, hosts, empleyee names, open ports and banners from different publicsh source (e.g. search engines, PSG key and SHODAN computer DB, Google, Bing, etc) and extract valuable information from the target domain.

```bash
theHarvester -d microsoft.com -l 200 -b baidu 
#-d domain or company name, -l number of results, -b data source
```

### Gather personal information from various social networking sites using Sherlock

Sherlock, a powerful command line tool provided by Sherlock Project, can be used to find usernames across many social networks.

```
python3 sherlock.py Mario Rossi
```

{% embed url="https://github.com/sherlock-project/sherlock" %}

## Perform Website Footprinting

### Gather info about target website using Ping command line utility

#### Ping

```bash
ping <Target_IP> -f -l 1500 # -f switch sets the Do Not Fragment bit on the ping packet - l buffer size
#we can try to change value of TTL with flag -i and -n number of echo requests
```

Analyzing the output, if there're packets lost, we adjust the size or length of the packet, reducing -l value till to have 100% of packets sent!

```bash
ping <Target_IP> -f -l 1472
```

### Gather info about website using Photon

Photon is a Python script used to crawl a given target URL to obtain information such as URLs (email, social media, file, secret key and subdom). The extracted info can further be exported in JSON format.

```
python3 photon.py -u <http://Target_IP>
# -u specifies the target website, -l specifies level to crawl, -t specifies number of threads
# --wayback specifies using URLs from archive.org as seeds
python3 photon.py -u <http://Target_IP> -l 3 -t 200 --wayback
```

{% embed url="https://github.com/s0md3v/Photon" %}

### Gather info about a target website using Central Ops

CentralOps is a free online network scanner that investigates domain and IP addresses, DNS records, traceroute, nslookup, whois searches, etc.

{% embed url="https://centralops.net/co/" %}

### Mirroring website using HTTrack Web Site Copier

It allows you to download a World Wide Web site from the Internet to a local directory, building recursively all directories, getting HTML, images, and other files from the server to your computer. HTTrack arranges the original site's relative link-structure. Simply open a page of the "mirrored" website in your browser, and you can browse the site from link to link, as if you were viewing it online.

Using Scan Rules tab we can add custom file format to select.

After downloading all, we can press Browse Mirrored Website to see website dumped.

## Perform Email Footprinting

### Gather info about a target by tracing emails using eMailTrackerPro

[https://emailtrackerpro.software.informer.com/download/](https://emailtrackerpro.software.informer.com/download/)

[https://www.youtube.com/watch?v=5Y7rJ\_iBaGE](https://www.youtube.com/watch?v=5Y7rJ\_iBaGE)

**Other Email Tracking Tools**

* Infoga
* Mailtrack

## Perform Whois Footprinting

### DomainTools

DomainTools website permits to perform Whois lookup on a website URL.

{% embed url="https://whois.domaintools.com/" %}

**Other Tools**

* SmartWhois
* Batch IP Converter

## Perform DNS Footprinting

### Gather DNS infor using nslookup command line utility and online tool

**Nslookup** is a network administration command-line utility, generally used for querying the DNS to obtain a domain name or IP address mapping or for any other specific DNS record. The utility is available both as a command-line utility and web app.

It's possible to do nslookup to query for the IP address of given domain setting type=a and take a CNAME lookup directly against the domain's authoritative name server and lists the CNAME record for a domain.

```bash
nslookup
set type=a #Configure nslookup to query for IP address of the domain
<Target_IP>
set type=cname #List the CNAME records for a domain
<Target_IP>
```

{% embed url="http://www.kloth.net/services/nslookup.php" %}

### Perform reverse DNS lookup using Reverse IP domain check and DNSRecon

DNS Lookup is used for finding the IP addresses for a given domain name, and the reverse DNS operation is performed to obtain the domain name of a given IP address.

Using Reverse IP Domain Check tool we can find the other domains/sites that share the same web server as our target server.

{% embed url="https://www.yougetsignal.com/" %}

## Perform Network Footprinting

### Locate the network range

Network range info assists in creating a map of the target network.

We can use ARIN Whois db search tool to do it.

{% embed url="https://www.arin.net/" %}

### Perform network tracerouting in Windows and Linux machines

#### Tracert

Traceroutes the network configuration information on the target domain

```bash
tracert <Target_IP>
tracert -h 5 <Target_IP> #-h number of hops allowed
```

There's an additional  online tool called SolarWinds.

{% embed url="https://www.solarwinds.com/" %}

### Perform advanced network route tracing using Path Analyzer Pro

Path Analyzer Pro performs network route tracing with performance test, DNS, Whois and network resolution to investigate network issues.

Network route tracing can determine the intermediate nodes traversed towards the destination and can detect the complete route (path) from source to destination.

* Set Protocol -> ICMP
* Target -> \<Target\_IP>
* Port -> 65535
* Time to trace -> 3 min

Stop or wait finish, and see report, synopsis log stats and others output.

If we want, there's an option to export result in .csv file format.

## Perform Footprinting using Various Footprinting Tools

### Footprinting a target using Recon-ng

Recon-ng is a web reconnaissance fw with indipendent modules and db interaction that provides an environment in which open-source web-based reconnaissance can be conducted.

* marketplace install all -> install all modules
* modules search -> displays all modules
* workspaces create -> create a new workspace
* workspaces list -> list your available workspaces
* db insert domains -> add a domain to the database to search
* modules load brute -> view all modules related to brute forcing

{% embed url="https://hackertarget.com/recon-ng-tutorial/" %}

{% embed url="https://securitytrails.com/blog/recon-ng" %}

{% embed url="https://github.com/Samsar4/Ethical-Hacking-Labs/blob/master/1-Footprinting-and-Reconnaissance/3-Recon-ng.md" %}

### Footprinting a target using Maltego

Maltego is a footprinting tool used to gather maximum information for the purpose of EH, computer forensics, and pentesting. It provides a library of transforms to discover data from open sources and visualize them in a graph format.

{% embed url="https://www.maltego.com/blog/beginners-guide-to-maltego-charting-my-first-maltego-graph/" %}

{% embed url="https://www.stationx.net/how-to-use-maltego/" %}

### Footprinting a target using OSINT Framework

OSINT Framework is an open-source intelligence gathering framework that helps security professionals for performing automated footprinting and reconnaissance, OSINT research and intelligence gathering.

{% embed url="https://osintframework.com/" %}
