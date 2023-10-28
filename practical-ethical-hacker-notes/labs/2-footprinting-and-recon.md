# 2 - Footprinting & Recon

## Module 02 - Footprinting and Reconnaissance

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

### Gather information about target website using Ping command line utility

### Ping

```bash
ping <Target_IP> -f -l 1500 # -f switch sets the Do Not Fragment bit on the ping packet - l buffer size
#we can try to change value of TTL with flag -i and -n number of echo requests
```

Analyzing the output, if there're packets lost, we adjust the size or length of the packet, reducing -l value till to have 100% of packets sent!

```bash
ping <Target_IP> -f -l 1472
```

### Gather information about website using Photon

Photon is a Python script used to crawl a given target URL to obtain information such as URLs (email, social media, file, secret key and subdom). The extracted info can further be exported in JSON format.

```
python3 photon.py -u <http://Target_IP>
# -u specifies the target website, -l specifies level to crawl, -t specifies number of threads
# --wayback specifies using URLs from archive.org as seeds
python3 photon.py -u <http://Target_IP> -l 3 -t 200 --wayback
```

{% embed url="https://github.com/s0md3v/Photon" %}

### Gather information about a target website using Central Ops

CentralOps is a free online network scanner that investigates domain and IP addresses, DNS records, traceroute, nslookup, whois searches, etc.

{% embed url="https://centralops.net/co/" %}

### Mirroring website using HTTrack Web Site Copier

It allows you to download a World Wide Web site from the Internet to a local directory, building recursively all directories, getting HTML, images, and other files from the server to your computer. HTTrack arranges the original site's relative link-structure. Simply open a page of the "mirrored" website in your browser, and you can browse the site from link to link, as if you were viewing it online.

Using Scan Rules tab we can add custom file format to select.

After downloading all, we can press Browse Mirrored Website to see website dumped.

## Perform Email Footprinting

### Gather information about a target by tracing emails using eMailTrackerPro

[https://emailtrackerpro.software.informer.com/download/](https://emailtrackerpro.software.informer.com/download/)

[https://www.youtube.com/watch?v=5Y7rJ\_iBaGE](https://www.youtube.com/watch?v=5Y7rJ\_iBaGE)

## Perform Whois Footprinting

### Perform Whois Lookup using DomainTools

DomainTools website permits to perform Whois lookup on a website URL.

{% embed url="https://whois.domaintools.com/" %}

In addition, there're whois lookup tools such as: SmartWhois and Batch IP Converter to extract additional target informations.

## Perform DNS Footprinting

### Gather DNS information using nslookup command line utility and online tool

Nslookup is a network administration command-line utility, generally used for querying the DNS to obtain a domain name or IP address mapping or for any other specific DNS record. The utility is available both as a command-line utility and web app.

It's possible to do nslookup to query for the IP address of given domain setting type=a and take a CNAME lookup directly against the domain's authoritative name server and lists the CNAME record for a domain.

```bash
nslookup
set type=a
<Target_IP>
set type=cname
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
tracert -h 5 <Target_IP> #maximum 5 hops allowed
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

### Perform Footprinting using Various Footprinting Tools

### Footprinting a target using Recon-ng

Recon-ng is a web reconnaissance fw with indipendent modules and db interaction that provides an environment in which open-source web-based reconnaissance can be conducted.

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
