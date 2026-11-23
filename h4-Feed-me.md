# h4 Feed me

This is the report for fourth assignment for the course cyber security - https://terokarvinen.com/cyber-security/

---

### x) Why would you want to use a feed reader (and RSS/Atom)? Couldn't you just browse to each website?

using an RSS/Atom feed reader provides several significant advantages Instead of manually navigating to individual cybersecurity blogs and news websites every day. some of the reasons/advantage are;

- Centralized Content Aggregation: The need to bookmark and manually browse multiple websites are eliminated when articles from dozens of security blogs, research feeds, and advisory portals are pulled into a single unified inbox.
- Privacy & Reduced Overhead: Reading posts through an RSS reader aid with bypassing invasive tracking scripts, advertising cookies, and heavy JavaScript rendering engines associated with full browser navigation.
- Operational Efficiency: A feed reader can continuously polls RSS XML endpoints in the background, allowing me to quickly scan new headlines and summaries in minutes without missing critical updates.
- Chronological & Unfiltered Feed: Unlike social media algorithms that manipulate content reach based on engagement metrics, RSS readers present posts strictly in chronological order.

### y) Supreme court of Finland, case Osuuspankkikeskus port scan KKO:2003:36. Have a brief look, summarize the key thing in a couple of bullets or sentences.

Here is my brief analysis of the Supreme Court of Finland precedent KKO:2003:36 (decided on April 8, 2003) regarding an unauthorized port scan against the Osuuspankkikeskus (OPK) banking network:

- **Case Facts:** On November 23, 1998, a 17-year-old individual used an automated port scanning tool to scan all IP addresses across the banking cooperative's network to locate open proxy servers. The scan was blocked by the bank's security firewall and did not penetrate the inner network.
- **Legal Ruling:** The Supreme Court held that systematic port scanning conducted with the intention of uncovering system vulnerabilities to gain unauthorized access constitutes an attempted data break-in (tietomurron yritys) under Chapter 38, Section 8 of the Finnish Criminal Code (RL 38:8). The court clarified that active network probing is legally equivalent to attempting an unauthorized intrusion.
- **Financial Compensation:** The Supreme Court ordered the defendant to pay full damages totaling 75,000 FIM (20,000 FIM to the cooperative and 55,000 FIM to its IT system operator) to cover investigation fees and external security auditing costs. The court ruled that compensation could not be reduced due to youth or lack of target awareness, emphasizing that individuals probing network perimeter security are fully liable for foreseeable investigation expenses triggered by their actions.

### a) Installing a feed reader and adding feeds

To configure Mozilla Thunderbird as my RSS feed reader inside Debian 13:
I Open the terminal and install Thunderbird:
i followed the instruction for this step in h4 tips (https://terokarvinen.com/cyber-security/#agenda). though i encounter a problem as seen in the screenshot below. then i asked Gemini how to solve this and followed the steps and instruction also below then i finally was able to install and lunch Thunderbird. 
<img width="1152" height="1211" alt="WhatsApp Image 2026-11-23 at 05 37 09" src="https://github.com/user-attachments/assets/273d48c2-3d5f-41d0-a466-8fc30e9d4682" />

It Started the installation process.
Requested a Debian DVD/CD image from /media/cdrom/ at one point.
The important part is that the terminal is still showing installation activity and media prompts, so i needed need to finish the process first.

_Suggested Steps_
- *Step 1* — Stop the DVD prompt
If the terminal is currently waiting for you to insert a disc, press:
Ctrl + C
This safely cancels the current installation attempt.
- *Step 2* — Fix Debian's package source
Type this command:
Look for a line beginning with deb cdrom:.
If you find it, put a # at the beginning of that line to disable it. Save using:
Ctrl + O → Enter
Ctrl + X
- *Step 3* — Update package lists

sudo apt-get update

sudo apt-get install -y thunderbird

<img width="1416" height="1432" alt="WhatsApp Image 2026-11-23 at 05 46 11" src="https://github.com/user-attachments/assets/3b9c3749-d205-481f-8688-2598fe030e23" />

### b) Added the feeds for Krebs using 

[Krebs on Security](https://krebsonsecurity.com/) with this https://krebsonsecurity.com/feed/

### C) Schneier on Security

The second required source was [Schneier on Security](https://www.schneier.com/).
Atom feed: `https://www.schneier.com/feed/atom/`

### d) Two additional cybersecurity feeds

I found them by performing google search with words like feeds for cyber security blogs for RSS feed and also asking Gemini to suggest me interesting feeds in cyber security area. 

**The Hacker News:** Added feed URL 'https://feeds.feedburner.com/TheHackersNews'.
i chose this because it Provides real-time coverage of major data breaches, software vulnerabilities, and zero-day exploits. which directly relates to the course.

**CISA Cybersecurity Advisories:** Added feed URL 'https://www.cisa.gov/cybersecurity-advisories/all.xml'.
I chose this because it is an Official federal feed delivering technical advisories and mitigation guidance for enterprise systems. also relates alot to the course topics and i have interest in it.
<img width="1482" height="1586" alt="WhatsApp Image 2026-11-23 at 06 06 26" src="https://github.com/user-attachments/assets/6f186b41-743b-496f-8919-11d2924784e2" />


### e) Following security feeds for a while.

Following cybersecurity feeds provided me with immediate awareness of major industry events:

- *Supply Chain Exploitation:* Analyzed how attackers exploited an Optimizely vendor vulnerability to inject data-stealing malware into 178 top websites (including BBC, CNN, and Zoom).
- *Cybercrime Indictments:* Tracked federal fraud charges against a ransomware recovery company that secretly paid extortions while charging victims marked-up fees.
- *Threat Group Operations:* Monitored Russian ransomware operations like Qilin and tracked Microsoft Patch Tuesday releases resolving over 1,100 security bugs.

**Comparison: RSS Readers vs. Alternative Tracking Methods**

**Benefits of RSS:** Eliminates algorithmic bias, speeds up news triage, preserves privacy, and works reliably across low-bandwidth connections.

**Downsides of RSS:** Some publishers truncate full article text requiring browser visits, feeds lack interactive community discussion/comments, and reader subscriptions require periodic management to avoid feed fatigue.

### f) Port scan

**Service Reconnaissance by Attackers:** Attackers discover running services on target networks by executing automated port scans using tools such as Nmap across public IP ranges. Port scanners transmit specialized TCP/UDP probe packets to identify open ports, active daemons (e.g., SSH, HTTP), operating system details, and exact software versions, which attackers compare against public vulnerability databases (CVEs) to locate exploit vectors.

Testing Procedure on Debian 13 VM
*Step 1: Install Nmap:* I Executed the following command in the Debian 13 VM terminal:

sudo apt-get update
sudo apt-get install -y nmap

*Step 2: Disconnect Internet & Verify Isolation*

In VirtualBox, navigate to Devices -> Network and uncheck Connect Network Adapter (or set Adapter to Not Attached).
Verify network isolation by pinging a public DNS address:
ping -c 3 8.8.8.8
Result: Terminal outputs ping: connect: Network is unreachable, confirming complete offline isolation.

though before disconnecting i first downloaded (without installing)  Apache2 packages, To avoid problems with APT while offline. so I downloaded Apache2 packages without installing them with:

*sudo apt install --download-only apache2*

Then disconnect computer from internet and run Ping 1.1.1.1 to confirm. now that it is offline i then run nmap against localhost with arguments -A to enable OS and version detection and -v to increase verbosity level.

<img width="1386" height="908" alt="WhatsApp Image 2026-11-23 at 07 58 42" src="https://github.com/user-attachments/assets/b3ea2554-2cab-4a25-b900-d635bba8ed47" />


*sudo nmap -A -v localhost*

after this i then proceeded with 

Install and Start Apache HTTP Daemon with this below

sudo apt-get install -y apache2
sudo systemctl start apache2
sudo systemctl status apache2

**Analysis Before Installing the Daemon**

Command Executed: sudo nmap -A -v localhost

*Results:*
Nmap scanned 1,000 standard TCP ports on 127.0.0.1 and found only 1 open port: Port 631/tcp

The remaining 999 TCP ports were closed (connection reset)

Service Identification: Port 631 was identified as running CUPS 2.4 (Internet Printing Protocol daemon).
Nmap's service probe (-A) grabbed the service banner CUPS/2.4 IPP/2.1 and the web interface title "Home - CUPS 2.4.10"

**Analysis After Installing the Daemon**

Command Executed: sudo nmap -A -v localhost

*Results:*
Nmap identified 2 open ports: Port 80/tcp and Port 631/tcp

The number of closed ports dropped to 998

New Service Identified: Port 80/tcp appeared as open, hosting an HTTP server

Banner & Version Grab: The aggressive scan (-A) retrieved the HTTP server header Apache/2.4.71 (Debian) and extracted the default page title "Apache2 Debian Default Page: It works" along with supported HTTP methods (GET POST OPTIONS HEAD)

**Conclusion**

Before launching Apache, TCP port 80 refused connections because no background process was bound to it. Starting the Apache daemon opened port 80 to accept HTTP requests. This comparison clearly demonstrates how port scanners discover active network services and exact software versions exposed by host daemons

### References

Finnish Supreme Court Case (KKO:2003:36)
Title: KKO:2003:36 | 8.4.2003 | Ennakkopäätökset | Korkein oikeus | Finlex
Link: https://www.finlex.fi/fi/oikeuskaytanto/korkein-oikeus/ennakkopaatokset/2003/36

Krebs on Security
Author: Brian Krebs: Feed URL: https://krebsonsecurity.com/feed/
Website: https://krebsonsecurity.com/

Schneier on Security
Author: Bruce Schneier: Feed URL: https://www.schneier.com/feed/
Website: https://www.schneier.com/

The Hacker News: Cybersecurity Feed: https://feeds.feedburner.com/TheHackersNews

CISA (Cybersecurity and Infrastructure Security Agency)
Advisories Feed: https://www.cisa.gov/cybersecurity-advisories/all.xml

Cyber Security Course Assignment Tero Karvinenen https://terokarvinen.com/cyber-security/#agenda

