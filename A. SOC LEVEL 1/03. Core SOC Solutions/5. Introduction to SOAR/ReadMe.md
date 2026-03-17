# Introduction to SOAR<br>(Security Orchestration, Automation, and Response)

To defend against attacks, a SOC team relies on various security solutions, such as SIEM, EDR, firewalls, and threat intelligence platforms. 

They also communicate with IT and management teams as part of their processes. 

However, as threats grow more complex and advanced, SOC teams face challenges like alert fatigue, manual processes, too many disconnected tools, and difficulties in communication across teams.

The SOAR tool overcomes these challenges for a SOC team.

---

Organisations have a Security Operations Center (SOC) as a centralised location for monitoring and protecting their digital assets. 

The main advantage of a SOC is to enhance an organisation's security incident handling through continuous monitoring and analysis. 

This is achievable by implementing the right amount of people, processes, and technologies to support the SOC's capabilities and business goals.


## Some key capabilities of a SOC:

1. **Monitoring and Detection:** 

Continuously scanning and flagging suspicious activities within a network environment. 

Leads to awareness of emerging threats and how to prevent them in their early stages. 

Done through the SIEM. 


2. **Recovery and Remediation:** 

Organisations rely on their SOC to provide a hub for recovery and remediation when incidents occur. 

SOC teams operate as first responders when cyber threats are identified. 

They perform operations such as:
- isolating infected endpoints, or
- shutting down infected endpoints,
- removing malware, and
- stopping malicious processes. 

During this process, they often utilize other security solutions like EDR, firewalls, IAM, etc to isolate an endpoint through EDR, block an IP on the firewall, disable a user on the IAM. 

3. **Threat Intelligence:** 

Monitoring environments continuously requires a constant flow of threat intelligence to ensure that SOC teams have continuous and the latest feeds of threat data, such as IP addresses, hashes, domains, and other indicators. 

4. **Communication:**

The SOC teams not only detect and respond to threats but also coordinate with IT teams and management to effectively communicate the threats and ensure that the incidents are addressed.
For example, generating a ticket for the IT team to verify a recently deployed patch.

In all these tasks, SOC works on multiple tools and communicates with various teams to carry out its processes thus may face some challenges!

## Challenges Faced by SOCs

- **Alert Fatigue:** Using numerous security tools triggers a large number of alerts within a SOC, many false positives or insufficient for an investigation. This leaves analysts overwhelmed and unable to address any serious security events.
- **Too many Disconnected Tools:** Security tools are often deployed without integration within an organisation. Security teams are tasked with navigating through firewall logs and rules, which are handled independently from endpoint security logs. This also leads to an overload of tools.
- **Manual Processes:** SOC investigation procedures are often not documented, leading to inefficient means of addressing threats. Most rely on established tribal knowledge built by experienced analysts, and the processes are never documented. This results in slowing down the investigation and increasing response times.
- **Talent Shortage:** SOC teams find recruiting and expanding their talent pool difficult to address the growing security landscape and sophisticated threats. 

---

# The SOAR Solution

Security Orchestration, Automation, and Response (SOAR) unifies all the security tools used in a SOC. 

With SOAR, SOC analysts do not need to switch between SIEM, EDR, Firewall, and other security tools for their investigations but can operate all these tools within a single SOAR interface. 

Along with unifying the security tools, it also provides ticketing and case management features to document, track, and resolve incidents in a structured way.

<img width="872" height="415" alt="image" src="https://github.com/user-attachments/assets/1c280f8a-0319-498e-85fc-2643fc2af30e" />

The core strength of a SOAR tool comes from the following three main capabilities:

1. **Orchestration**
2. **Automation**
3. **Response**

<img width="842" height="429" alt="image" src="https://github.com/user-attachments/assets/45adf704-9952-4779-bd84-ea0b3f0896ce" />


---

## Building SOAR Playbooks

**Playbooks**: Pre-defined documented steps of handling and incident.

**SOAR Playbooks** Pre-defined workflows that tell the SOAR tool what actions to take during a specific investigation. 

SOC analysts make playbooks for a general category of recurring alerts. 

sample playbooks for:
1. Phishing
2. CVE Patching. 

### Phishing Playbook

<img width="787" height="614" alt="image" src="https://github.com/user-attachments/assets/0a18b4a9-a677-43e0-bc11-7dd7ec57b307" />


### CVE Patching Playbook

<img width="1354" height="440" alt="image" src="https://github.com/user-attachments/assets/83132630-a084-4711-88cb-77e317cae24a" />


