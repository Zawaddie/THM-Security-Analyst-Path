# Introduction to SIEM

Security Information and Event Management system (SIEM) is the core security solution that a SOC analyst uses in the security operations center.

---

 A simple network that comprises multiple Linux/Windows-based Endpoints, one data server, and one website.

<img width="855" height="421" alt="image" src="https://github.com/user-attachments/assets/a0c4ebc1-42df-4936-8e2e-d6cad7a5fb0a" />


These devices in the  network communicate with each other and with the Internet through a router . They continuously generate logs that serve as a trail of all the activities and are extremely helpful for identifying malicious activities or general troubleshooting. 

---

**CATEGORIES OF LOG SOURCES:**

1) **Host-Centric Log Sources**
   
These log sources capture events that occurred within or related to the host. 
Devices that generate host-centric logs: **Windows, Linux, servers, etc. 

Some examples of host-centric logs are:

- A user accessing a file
- A user attempting to authenticate.
- A process execution activity
- A process adding/editing/deleting a registry key or value.
- PowerShell execution

2) **Network-Centric Log Sources**

Network-related logs are generated when the hosts communicate with each other or access the internet to visit a website. 
Devices that generate network-centric logs: **firewalls, IDS/IPS, routers, etc. 

Some examples of network-centric logs are:

- SSH connection
- A file being accessed via FTP
- Web traffic
- A user accessing the company's resources through VPN.
- Network file sharing Activity



Together, these host-centric and network-centric log sources constantly create numerous logs in a network. 

These log sources generate logs, we analyze them, and identify malicious activities.

However challenges can be:

- Numerous Log Sources
- No Centralization and would require to connect to individual device to analyze logs
- Limited Context Individual since logs cannot tell the whole story of an activity.
- Limited Analysis, is nearly impossible for humans, if analyzing all the logs from all the devices is done manually to identify any abnormal activity .
- Format Issues since Different log sources generate logs in various formats.

SIEM Tool is a powerful technology that can solve all these problems.

<img width="811" height="471" alt="image" src="https://github.com/user-attachments/assets/851d59af-a79f-424b-acb8-96431cda8277" />

---

**FEATURES OF SIEM**

Provides capabilities to enhance security operations:

- Centralized Log Collection
- Normalization of Logs: A Windows logs & Linux logs are different when raw but in SIEM they are broken down into different fields and presented in one consistent format. Breaking down a log into several fields for ease of understanding is known as Parsing, and converting all the logs of various log sources into one consistent format is known as Normalization.
- Correlation of Logs of different sources and finds any relationship between them to helps to identify malicious activity by analyzing its pattern.
- Real-time Alerting after SIEM detects malicious activities based on the rules it contains and analysts can then investigate these alerts within the SIEM platform.  
- Dashboards and Reporting: SIEM presents the data for analysis after being normalized and ingested. Dashboards presents the summary of this analysis in the form of actionable insightss.

Below is some of the information that can be found in a dashboard:
  - Alert Highlights
  - System Notification
  - Health Alert
  - List of Failed Login Attempts
  - Events Ingested Count
  - Rules triggered
  - Top Domains Visited

---

<img width="763" height="501" alt="image" src="https://github.com/user-attachments/assets/153b725b-1714-44ff-8120-e7c7d760111b" />

**LOG INGESTION**

All these logs provide a wealth of information and can help identify security issues. 
Each SIEM solution has its own way of ingesting the logs. 

Some common methods of ingesting the logs:

- **Agent / Forwarder**

These SIEM solutions provide a lightweight tool called an agent (forwarder by Splunk) that gets installed on the Endpoint. 
It is configured to capture and send all the important logs to the SIEM server.

- **Syslog**

Syslog is a widely used protocol to collect data from various systems like web servers, databases, etc., and send real-time data to the centralized destination.

- **Manual Upload**

Some SIEM solutions, like Splunk, ELK, etc., allow users to ingest offline data for quick analysis. Once the data is ingested, it is normalized and made available for analysis.

- **Port-Forwarding**

SIEM solutions can also be configured to listen on a certain port, and then the endpoints forward the data to the SIEM instance on the listening port.

An example of how Splunk provides various methods for log Ingestion:

<img width="1264" height="389" alt="image" src="https://github.com/user-attachments/assets/ce5c049d-8b05-4016-986b-c79b2cfcf55a" />

---

**ALERTING PROCESS AND ANALYSIS**

A SIEM solution detects threats by correlating logs from the log sources and triggers alerts, Behind the Triggered Alerts the SIEM solution has detection rules that catch threats and play an important role in the timely detection of threats, allowing analysts to take action on time. 

Detection rules are pretty much logical expressions set to be triggered. 

A few examples of detection rules are:

- If a user gets five failed Login Attempts in 10 seconds, raise an alert for Multiple Failed Login Attempts
- If login is successful after multiple failed login attempts, raise an alert for Successful Login After multiple Login Attempts
- A rule is set to alert every time a user plugs in a USB (Useful if USB is restricted as per the company policy)
- If outbound traffic is > 25 MB, raise an alert to potential data exfiltration Attempt (Usually, it depends on the company policy)


**CREATION OF DETECTION RULES**

To explain how the rule works, consider the following Eventlog use cases:

**Use-Case 1:**

Adversaries tend to remove the logs during the post-exploitation phase to remove their tracks. 
A unique Event ID 104 is logged every time a user tries to remove or clear event logs. 
To create a rule based on this activity, we can set the condition as follows:

Rule: If the Log source is WinEventLog AND EventID is 104 - Trigger an alert Event Log Cleared

**Use-Case 2:**

Adversaries use commands like whoami after the exploitation/privilege escalation phase. 
The following Fields will be helpful to include in the rule.
- Log source: Identify the log source capturing the event logs
- Event ID: Which Event ID is associated with Process Execution activity? In this case, Event ID 4688 will be helpful.
- NewProcessName: Which process name will be helpful to include in the rule?

Rule: If Log Source is WinEventLog AND EventCode is 4688, and NewProcessName contains whoami, then Trigger an ALERT WHOAMI command Execution DETECTED

In the previous task, the importance of field-value pairs was discussed. Detection rules keep an eye on the values of certain fields to get triggered. That is the reason why it is important to have normalized logs ingested.

**ALERT INVESTIGATION**

When monitoring SIEM, analysts spend most of their time on dashboards, as they display various key details about the network in a very summarized way. 
Once an alert is triggered, the events/flows associated with the alert are examined, and the rule is checked to see which conditions are met. 
Based on the investigation, the analyst determines if it's a True or False positive. 

Some of the actions that are performed after the analysis are:

- Alert is a False Positive. It may require tuning the rule to avoid similar False positives from occurring again.
- Alert is a True Positive. Perform further investigation.
- Contact the asset owner to inquire about the activity.
- Suspicious activity is confirmed. Isolate the infected host.
- Block the suspicious IP.

