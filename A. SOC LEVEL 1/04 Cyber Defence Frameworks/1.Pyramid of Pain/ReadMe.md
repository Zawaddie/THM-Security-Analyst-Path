# Pyramid of pain

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



---

### 3. **Domain Names**

Example:

* Malicious domain used for phishing or malware download.

Attackers may:

* Register new domains
* Use domain generation algorithms (DGAs)

🔹 **Pain to attacker:** Moderate
🔹 **Why:** Requires registering new domains and updating infrastructure.

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

✅ **Simple way to remember:**

| Level | Indicator | Attacker Pain |
| ----- | --------- | ------------- |
| 1     | Hash      | Very Low      |
| 2     | IP        | Low           |
| 3     | Domain    | Medium        |
| 4     | Artifacts | Medium-High   |
| 5     | Tools     | High          |
| 6     | TTPs      | Very High     |

---


