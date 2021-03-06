# Register on a Platform
[a relative link](/bugbounty101/Bug Bounty Platforms.md)

# Pick a Target
It is recommended to pick a target that's large and old. The new programs, websites, and companies are flooded with professionals who are have more experience and have fined tuned their tools to be efficient. A company like AT&T is expected to have tens of thousands of websites, links, sub-domains, etc. A lot of their code was written without regard to security and may have been lost or undocumented. These are the targets you want to look for. 

# Read the Scope/Rules of Engagement/Policy
Understand what you're allowed and not allowed to do. Generally DoS attacks are banned and would therefore be illegal hacking. Here's an example for Yahoo.com:

#### In-Scope Domains and Properties
The scope of this program is limited to technical security vulnerabilities on Yahoo owned applications. For password and account access issues please work with our Customer Care team. 
- *.yahoo.com
- *.flickr.com
- All Yahoo and Flickr branded mobile apps
- All Yahoo and Flickr branded client side applications
- Brightroll
- Flurry
- Polyvore
- Yahoo Small Business (aabaco and luminate domains)
#### Out-of-Scope Domains and Properties
- *.yahoo.net
- Yahoo 7 (au.yahoo.com/nz.yahoo.com)
- Yahoo Japan (Contact: yird-contact@mail.yahoo.co.jp)
- Tumblr
- Onwander
- Rivals
- Yahoo operated Wordpress blogs
- Media Group One

# Perform Recon

## Goal
- Look for sub domains (*.example.com)
- Look for mobile apps
- Look for acquisitions (6 mo. Rule)
  - Wikipedia (list of mergers and acquisitions)
- Look for change/re-designs
- Look for mobile sites

## Methods

### Sub Domain Enumeration
Create a list of domain names to use: [ADD MORE]

#### Tools
- [Subbrute](https://github.com/TheRook/subbrute) – A DNS meta-query spider that enumerates DNS records, and subdomains.
  - Usage: ./subbrute.py -p [example.com]
- [dnscan](https://github.com/rbsec/dnscan) – a python wordlist-based DNS subdomain scanner.
  - Usage: ./dnscan.py -d [example.com] -w [wordlist.txt]
- [Nmap](https://nmap.org/nsedoc/scripts/dns-brute.html) – Yes it’s a port scanner, but it can bruteforce subdomains too (check nmap scripts)
  - Usage: nmap --script=dns-brute [example.com]
- Recon-Ng – The recon-ng framework has a brute_hosts module that allows to bruteforce subdomains.
- DNSRecon – A powerful DNS enumeration script
- Fierce – A semi-lightweight enumeration scanner
- Gobuster – Alternative directory and file busting tool written in Go
- DNSenum – Offers recursive and threaded subdomain enumeration.
- AltDNS – offers bruteforcing based on permutations of already found domains
- Brutesubs - Automated framework for running multiple subdomain bruteforce tools at the same time. https://github.com/anshumanbh/brutesubs
- Enumail.sh - wrapper around Recon-Ng by Jason Haddix
- Sublist3r - (EDIT)

Automated Sub Domain Enumeration: <br />
> git clone https://github.com/aboul3la/Sublist3r.git <br />
> cd Sublist3r <br />
> python sublist3r -h <br />
Example: python sublist3r.py -d google.com

#### Find More Domains
Look for sites outside your list (but still in scope): <br />
- site: example.com
- Exclude sites you know about: -www.example.com -ftp.example.com

Look for Mergers and Acquisitions. Generally, six (6) months after a M&A, it's in scope. <br />
Example: https://history.gmheritagecenter.com/wiki/index.php/Category:Mergers_%26_Acquisitions

Look at bugs reports published for your target organization. This will help you understand what kind of vulnerabilities they the target will tend to have and what you should be looking for. If someone found three XSS on sub domains of your target, chances are you'll find more as the developer and QC process didn't catch them. <br />
Example: Facebook.com/notes/phwd/facebook-bug-bounty-/

### Organize Domains/Sub-Domains
The list of domains/sub-domains may be extensive, depending on the size of the target. First, merge the lists provide by the different tools/techniques used. The following may help remove duplicates from a text file: awk '!seen[$0]++' filename

Automate the enumeration of domains/sub-domains: https://github.com/ChrisTruncer/EyeWitness
Useage: 
> ./EyeWitness.py -f filename -t optionaltimeout --open (Optional)

# Scan The Target
Perform a port scan on your target. <br />
Example: nmap -sS -A -Pn -p- --script=http-title example.com

# Enumerate Web Servers
### NMAP Scans
- nmap -A -sS -Pn -p 80,443,8080 [example.com]
- nmap -A -sS -Pn -p 80,443,8080 [example.com] --script=http-enum
- nmap -A -sS -Pn -p 80,443,8080 [example.com] --script=http-methods
NMAP HTTP Libraries: https://nmap.org/nsedoc/lib/http.html

### Directory Enumeration
- DirBuster
- GoBuster
- SYN Digger
- Git Digger
- nmap --script=http-enum

Use directory list and RAFT lists: https://github.com/danielmiessler/SecLists/tree/master/Discovery/Web-Content

### Identify Platforms
- Wapplyzer (Chrome)
- Builtwith (Chrome)
- Retire.js (cmd-line or Burp)

### OSINT
Public disclosures that may not be submitted
- Xssed.com
- Reddit XSS /r/xss
- Punkspider
- Xss cx
- Xssposed.org
- Twitter

### Robots.txt
Check the website for /robots.txt

### Sitemap.xml
Check the website for /sitemap.xml
