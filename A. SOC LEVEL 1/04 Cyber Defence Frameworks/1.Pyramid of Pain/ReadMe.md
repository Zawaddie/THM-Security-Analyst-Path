# Pyramid of pain

<img width="1043" height="122" alt="image" src="https://github.com/user-attachments/assets/ab086a56-134b-47e5-944a-bd819d5170bb" />


This well-renowned concept is being applied to cybersecurity solutions like Cisco Security, SentinelOne, and SOCRadar to improve the effectiveness of CTI (Cyber Threat Intelligence), threat hunting, and incident response exercises.

Understanding the Pyramid of Pain concept as a Threat Hunter, Incident Responder, or SOC Analyst is important.

in a nutshell, the **Pyramid of Pain** is a concept in cybersecurity that shows **how difficult it is for attackers to change their tactics when defenders detect different types of indicators**. 
It was created by **David J. Bianco**.

The idea:

* **Indicators at the bottom are easy for attackers to change.**
* **Indicators at the top are hard for attackers to change.**
* The **higher up you detect them**, the **more pain you cause the attacker**.

---

## Structure of the Pyramid of Pain

| Level | Indicator    | Pain to Attacker |
| ----- | ------------ | ---------------- |
| 6     | TTPs         | Very High        |
| 5     | Tools        | High             |
| 4     | Artifacts    | Medium           |
| 3     | Domains      | Low–Medium       |
| 2     | IP Addresses | Low              |
| 1     | Hashes       | Very Low         |


```
          TTPs (Most Pain)
             ▲
            Tools
             ▲
      Network/Host Artifacts
             ▲
           Domains
             ▲
         IP Addresses
             ▲
         Hash Values
        (Least Pain)
```

---

### 1. **Hash Values (Bottom – Least Pain)**

(Trivial)

Examples: MD5, SHA256 file hashes.

* Used to identify **specific malware files**.
* Attackers can easily change a file slightly to create a **new hash**.

Example:

* Detecting a malware hash in **VirusTotal**.

🔹 **Pain to attacker:** Very low

🔹 **Why:** Just recompile or modify the file.

 an example of how you can change the hash value of a file by simply appending a string to the end of a file using echo: 
 
 File Hash (Before Modification)
 
```

PS C:\Users\THM\Downloads> Get-FileHash .\OpenVPN_2.5.1_I601_amd64.msi -Algorithm MD5
Algorithm Hash                             Path                                                 
_________ ____                             ____                                                 
MD5       D1A008E3A606F24590A02B853E955CF7 C:\Users\THM\Downloads\OpenVPN_2.5.1_I601_amd64.msi

```

File Hash (After Modification)

```

PS C:\Users\THM\Downloads> echo "AppendTheHash" >> .\OpenVPN_2.5.1_I601_amd64.msi
PS C:\Users\THM\Downloads> Get-FileHash .\OpenVPN_2.5.1_I601_amd64.msi -Algorithm MD5
Algorithm Hash                             Path                                                 
_________ ____                             ____                                                 
MD5       9D52B46F5DE41B73418F8E0DACEC5E9F C:\Users\THM\Downloads\OpenVPN_2.5.1_I601_amd64.msi

```

There are ransomware reports from the past, where security researchers  provide the hashes related to the malicious or suspicious files used at the end of the report. 

examples can be found in the below:
- [The DFIR Report](https://thedfirreport.com/)
- [Trellix Threat Research Blogs](https://www.trellix.com/blogs/research/) .

Various online tools can be used to do hash lookups like:
- [VirusTotal](https://www.virustotal.com/gui/)
- [Metadefender Cloud - OPSWAT](https://metadefender.opswat.com/?lang=en)

---

### 2. **IP Addresses**

(Easy)

Example:

* Detecting malicious IPs used for command-and-control (C2).

Attackers can:

* Switch servers
* Use cloud hosts
* Use botnets

🔹 **Pain to attacker:** Low

🔹 **Why:** They can quickly change infrastructure.

[ANY.RUN](https://app.any.run/) can be used  to check malacious IPs.

[ANY.RUN](https://app.any.run/) is an online malware analysis sandbox used by cybersecurity professionals to safely analyze suspicious files, links, or malware in a controlled virtual environment.

Instead of running a suspicious file on your own computer, you upload it to ANY.RUN and watch how it behaves in a virtual machine.

<img width="1355" height="725" alt="image" src="https://github.com/user-attachments/assets/e8bc68db-b361-4102-ad3f-b64ff770d5d2" />

One of the ways an adversary can make it challenging to successfully carry out IP blocking is by using **Fast Flux**.

According to [Akamai](https://www.akamai.com/blog/security/digging-deeper-an-in-depth-analysis-of-a-fast-flux-network), Fast Flux is a DNS technique used by botnets to hide phishing, web proxying, malware delivery, and malware communication activities behind compromised hosts acting as proxies. 

The purpose of using the **Fast Flux** network is to make the communication between malware and its command and control server (C2) challenging to be discovered by security professionals. 

So, the primary concept of a Fast Flux network is having multiple IP addresses associated with a domain name, which is constantly changing. 

Palo Alto created a great fictional scenario to explain Fast Flux: ["Fast Flux 101: How Cybercriminals Improve the Resilience of Their Infrastructure to Evade Detection and Law Enforcement Takedowns"](https://unit42.paloaltonetworks.com/fast-flux-101/)

---

### 3. **Domain Names**

(simple)

Example:

* Malicious domain used for phishing or malware download.

Attackers may:

* Register new domains
* Use domain generation algorithms (DGAs)

🔹 **Pain to attacker:** Moderate

🔹 **Why:** Requires registering new domains and updating infrastructure.

Domain Names can be a little more of a pain for the attacker to change as they would most likely need to purchase the domain, register it and modify DNS records. Unfortunately for defenders, many DNS providers have loose standards and provide APIs to make it even easier for the attacker to change the domain.

Malicious  Sodinokibi  C2 ( Command and Control Infrastructure)  domains:

<img width="1355" height="546" alt="image" src="https://github.com/user-attachments/assets/d5d3f3c1-add8-4f16-9b38-8dd762f57166" />

To detect malicious domains, proxy logs or web server logs can be used.
 
Attackers usually hide the malicious domains under URL shorteners that redirects to the specific website specified during the initial step of setting up the URL Shortener link.

Some URL-shortening services used by attackers to generate malicious links: 
 
- bit.ly
- goo.gl
- ow.ly
- s.id
- smarturl.it
- tiny.pl
- tinyurl.com
- x.co

You can see the actual website the shortened link is redirecting you to by appending "+" to it.

**Viewing Connections in Any.run:**

Because [Any.run]() is a sandboxing service that executes the sample, we can review any connections such as HTTP requests, DNS requests or processes communicating with an IP address by looking at the "networking" tab located just below the snapshot of the machine.

1. **HTTP Requests:**

This tab shows the recorded HTTP requests since the detonation of the sample. This can be useful to see what resources are being retrieved from a webserver, such as a dropper or a callback.

 
<img width="1071" height="259" alt="image" src="https://github.com/user-attachments/assets/f589d268-50d6-49d6-95c3-a8a386b8b642" />

illustrating the HTTP requests in the anyrun view

2. **Connections:**

This tab shows any communications made since the detonation of the sample. This can be useful to see if a process communicates with another host. For example, this could be C2 traffic, uploading/downloading files over FTP, etc.

<img width="1065" height="258" alt="image" src="https://github.com/user-attachments/assets/dedeaa1b-7a19-46d7-a769-e0fd98f16462" />

illustrating the connections in the anyrun view

3. **DNS Requests:**

This tab shows the DNS requests made since the detonation of the sample. Malware often makes DNS requests to check for internet connectivity (I.e. if It can't reach the internet/call home, then it's probably being sandboxed or is useless). 

<img width="1060" height="244" alt="image" src="https://github.com/user-attachments/assets/4bd53fd4-8a6b-400e-a4fa-189b27d12efc" />

illustrating the DNS requests in the anyrun view

**Punycode attack** uses Unicode characters in the domain name to imitate the a known domain.

---

### 4. **Network / Host Artifacts**

Examples:

* Specific registry keys
* File paths
* Mutex names
* Network patterns

These artifacts appear because of **how malware behaves** on a system.

🔹 **Pain to attacker:** Medium-high

🔹 **Why:** Requires rewriting parts of the malware.

Host artifacts are the traces or observables that attackers leave on the system, such as registry values, suspicious process execution, attack patterns or IOCs (Indicators of Compromise), files dropped by malicious applications, or anything exclusive to the current threat.


Network Artifacts also belong to the yellow zone in the Pyramid of Pain. This means if you can detect and respond to the threat, the attacker would need more time to go back and change his tactics or modify the tools, which gives you more time to respond and detect the upcoming threats or remediate the existing ones.

A network artifact can be a user-agent string, C2 information, or URI patterns followed by the HTTP POST requests.An attacker might use a User-Agent string that hasn’t been observed in your environment before or seems out of the ordinary. 
The User-Agent is defined the request-header field that contains the information about the user agent originating the request.

Network artifacts can be detected in Wireshark PCAPs by using a network protocol analyzer such as [TShark](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) or exploring IDS (Intrusion Detection System) logging from a source such as [Snort](https://www.snort.org/).

HTTP POST requests containing suspicious strings:

<img width="1356" height="120" alt="image" src="https://github.com/user-attachments/assets/65cd5680-dca2-4b93-8b38-6c38a13dfac8" />

we use TShark to filter out the User-Agent strings by using the command:

```
tshark --Y http.request -T fields -e http.host -e http.user_agent -r analysis_file.pcap 

```

<img width="1346" height="328" alt="image" src="https://github.com/user-attachments/assets/3d3cc75a-8222-4bbe-b280-fcf7023b4d90" />

These are the most common User-Agent strings found for the [Emotet Downloader Trojan](https://www.mcafee.com/blogs/other-blogs/mcafee-labs/emotet-downloader-trojan-returns-in-force/)

If you can detect the custom User-Agent strings that the attacker is using, you might be able to block them, creating more obstacles and making their attempt to compromise the network more annoying.


    
---

### 5. **Tools**

Examples:

* Malware families
* Exploitation frameworks

Examples of tools:

* Cobalt Strike
* Metasploit
* Mimikatz

🔹 **Pain to attacker:** High

🔹 **Why:** They must change tools or develop new ones.


At this stage, we have levelled﻿ up our detection capabilities against the artifacts. The attacker would most likely give up trying to break into your network or go back and try to create a new tool that serves the same purpose. It will be a game over for the attackers as they would need to invest some money into building a new tool (if they are capable of doing so), find the tool that has the same potential, or even gets some training to learn how to be proficient in a certain tool. 

Attackers would use the utilities to create malicious macro documents (maldocs) for spearphishing attempts, a backdoor that can be used to establish C2 (Command and Control Infrastructure)(opens in new tab), any custom .EXE, and .DLL files, payloads, or password crackers.

A Trojan dropped the suspicious "Stealer.exe" in the Temp folder:

<img width="965" height="443" alt="image" src="https://github.com/user-attachments/assets/56cb2f62-2491-448e-9505-160271eb069b" />

The execution of the suspicious binary:

<img width="817" height="51" alt="image" src="https://github.com/user-attachments/assets/5ce78d55-8997-4220-8767-2cf12c6ac0ce" />

Antivirus signatures, detection rules, and YARA rules can be great weapons for you to use against attackers at this stage.

[MalwareBazaar](https://bazaar.abuse.ch/) and [Malshare](https://malshare.com/) are good resources to provide you with access to the samples, malicious feeds, and YARA results - these all can be very helpful when it comes to threat hunting and incident response. 

For detection rules, [SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/) is a great platform, where security professionals share their detection rules for different kinds of threats including the latest CVE's that are being exploited in the wild by adversaries. 

**Fuzzy hashing** is also a strong weapon against the attacker's tools. Fuzzy hashing helps you to perform similarity analysis - match two files with minor differences based on the fuzzy hash values. One of the examples of fuzzy hashing is the usage of [SSDeep](https://ssdeep-project.github.io/ssdeep/index.html); on the SSDeep official website, you can also find the complete explanation for fuzzy hashing. 

Example of SSDeep from VirusTotal:

<img width="1111" height="607" alt="image" src="https://github.com/user-attachments/assets/d8d97e91-e0c3-4ad9-9e84-007e075df18e" />

Method to determine file similarity: Fuzzy Hashing.

Alternative name for fuzzy hashes: Context Triggered Piecewise Hashes

---

### 6. **Tactics, Techniques, and Procedures (Top – Most Pain)**

These are the **behavior patterns** attackers use.

Framework used to categorize them:

* MITRE ATT&CK

Examples:

* Credential dumping
* Lateral movement
* Privilege escalation

🔹 **Pain to attacker:** Very high

🔹 **Why:** They must **change their entire attack methodology**.

TTPs: Tactics, Techniques & Procedures. This includes the whole [MITRE ATT&CK Matrix](https://attack.mitre.org/), which means all the steps taken by an adversary to achieve his goal, starting from phishing attempts to persistence and data exfiltration. 

If you can detect and respond to the TTPs quickly, you leave the adversaries almost no chance to fight back. For, example if you could detect a [Pass-the-Hash](https://www.beyondtrust.com/resources/glossary/pass-the-hash-pth-attack) attack using Windows Event Log Monitoring and remediate it, you would be able to find the compromised host very quickly and stop the lateral movement inside your network. 

At this point, the attacker would have two options: Go back, do more research and training, reconfigure their custom tools orGive up and find another target


---

## Visual Representation



---

## Why the Pyramid Matters (SOC / Threat Hunting)

If you're doing **SOC analysis or threat hunting** (like using **Elastic Stack** or **Kibana**), focusing only on **hashes or IPs** is weak detection.

Better detection focuses on:

* **Behavior**
* **Attack techniques**
* **Adversary tactics**

Example:
Instead of blocking:

```
IP: 185.x.x.x
```

Detect:

```
Process spawning PowerShell → downloading payload → credential dumping
```

---

You can pick any APT (Advanced Persistent Threat Groups) as another exercise. A good place to look at would be [Rapid7 Advanced Persistent Threat Groups](https://docs.rapid7.com/insightidr/apt-groups/). When you have determined the APT Group you want to research - find their indicators and ask yourself: " What can I do or what detection rules and approach can I create to detect the adversary's activity?", and "Where does this activity or detection fall on the Pyramid of Pain?”

 
As David Bianco states, "the amount of pain you cause an adversary depends on the types of indicators you are able to make use of". 
---


