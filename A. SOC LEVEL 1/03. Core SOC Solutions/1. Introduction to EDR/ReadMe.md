# Introduction to EDR:

From the room am able to:
- Understand the basics of EDR and how it works
- Differentiate EDR from traditional Antivirus solutions
- Examine the architecture of an EDR solution
- Analyze the types of telemetry it collects from endpoints
- Understand the detection and response capabilities of an EDR
- Investigate a realistic alert in the EDR

---

Endpoint Detection and Response (EDR) is a security solution that offers deep-level protection for endpoints.

some of the EDR solutions in the market:

1. [CrowdStrike Falcon](https://www.crowdstrike.com/wp-content/uploads/2022/03/crowdstrike-falcon-insight-data-sheet.pdf)
2. [SentinelOne ActiveEDR](https://sentinelone.com/resources/datasheets/assets/usecase/sentinel-one-active-#page=1)
3. [Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint)
4. [OpenEDR](https://www.openedr.com/)
5. [Symantec EDR](https://docs.broadcom.com/doc/endpoint-detection-and-response-atp-endpoint-en)

many morw EDR's available in the market but the Underlying architecture is similar:

---

**Three features of an EDR:**

<img width="763" height="270" alt="image" src="https://github.com/user-attachments/assets/3a15bb3a-b01f-4da3-99fe-6dca1b9be60b" />

EDR collects detailed data from the endpoints, which includes:
- process modifications,
- registry modifications,
- file and folder modifications,
- user actions, and much more.

EDR incorporates signature-based detections as well as behavior-based detections, such as unexpected user activities. 
With modern machine learning capabilities, it identifies any deviation from the baseline behavior and instantly flags it. 
It can also detect fileless malware that resides in memory. 
It also allows us to feed custom IOCs for threat detections.

EDR also empowers analysts to take action on detected threats. 
These actions can be taken at any endpoint within the central EDR console. 
Imagine getting a detection on the EDR with full-fledged details on when, where, and what happened, and you have to opt for the best possible action for that detection. 
As an analyst, you may decide to isolate a complete endpoint, terminate a process, or quarantine some files. 
You can also connect to the host remotely and execute actions independently. 
You can do this all from within the EDR console

<img width="825" height="382" alt="image" src="https://github.com/user-attachments/assets/59ba9545-3282-48ab-8bea-f6727ebb3b7b" />

We can integrate multiple endpoints with our EDR and manage them through a centralized console by deploying EDR agents in the endpoints.

---

**EDR Telemetry**

This is the data it collects from endpoints:

- Process Executions and Terminations
  
Running and idle processes.
Helps to identify suspicious child-parent process relationships, suspicious executables initiating a process, malware payload, etc.

- Network Connections
  
monitoring all endpoints' network connections.
Helps identify any connection to a C2 server, unusual port usage, data exfiltration, or lateral movement within the network.

- Command Line Activity
 
Captures all the commands executed on the endpoints in CMD/PowerShell/bash.
Helps to identify malicious command execution, obfuscated PowerShell script executions, which are often missed by a traditional antivirus.

- Files and Folders Modifications
  
The EDR tracks Files and Folders Modifications
Threat actors modify different files and folders during data staging, ransomware executions, and malicious file dropping. 

- Registry Modifications

The registry holds information about the configurations in a Windows system. 
Many registry modifications that occur during a malicious activity, 
The EDR monitors these.

EDR collects much more than this data from an endpoint using complex logic and machine learning algorithms to assess the activities. 

**NOTE**

Advanced threats keep most of their activities stealthy, using legitimate utilities during execution. Individually, their activities may seem harmless, but when observed through detailed telemetry, they tell a different story. This detailed telemetry not only helps the EDR detect advanced threats and make better judgments on the legitimacy of the activities, but it is also very helpful for the analysts during the investigations. The analysts can understand the full chain of events, identify the root cause, and reconstruct the attack timeline.


---

**ADVANCED DETECTION TECHNIQUES AND RESPONSES OF AN EDR:**

**Some advanced detection techniques applied to telemetry data include:**

- **Behavioral Detection**

Instead of just matching the signatures with known threats, it observes the complete behavior of a file. Advanced threats craft their malware to look clean and use legitimate processes to carry out their attack. EDR catches this behavior.

Example: A process winword.exe spawning PowerShell.exe will be flagged by the EDR due to the behavior. A Word document spawning a PowerShell is an unusual parent-child relationship.

- **Anomaly Detection**
  
With time, EDR understands the baseline behavior of the endpoints. Any activity that deviates from this behavior will be flagged. During any malicious activity, the endpoint's behavior deviates from normal. EDR picks it up. Sometimes, this can generate false positives as well. However, with the full context it gives, the analyst can identify its legitimacy.

Example: On one of the endpoints, a process modifies an auto-start registry key, which is not a common behavior on the endpoint.

- **IOC matching**

EDRs have some strong threat intelligence field integrations. Except for zero-day attacks, most of the attacks have indicators published in the threat intelligence feeds. EDR flags any activity that matches any known IOC.  

Example: A user downloads a file that drops an executable. The executable is often used in a specific attack. The hash of this executable will get matched with the threat intelligence feed and instantly flagged by the EDR.

- **MITRE ATT&CK Mapping**

Any activity flagged by the EDR is not only marked as malicious or suspicious but also mapped with the MITRE Tactic and Technique (attack stage) that the particular activity was on. This proves to be very helpful for the analysts.

Example: If the EDR flags the creation of a scheduled task for any reason, it will likely map this activity to:

Tactic: Persistence

Technique: Scheduled Task/Job

- **Machine Learning Algorithms**

Advanced threat actors try to evade defenses as much as possible, and their activities may sometimes bypass advanced detection techniques. Modern EDRs have machine learning models trained by a large dataset of normal and malicious behaviors. This can detect complex patterns of an attack.

Example: Attacks in which the individual actions are not inherently malicious, but the ML algorithm identifies the whole chain of activities as malicious. Fileless attacks and multi-staged intrusions are often detected through this.

---

**EDR OFFERS BOTH AUTOMATED AND MANUAL RESPONSES AFTER DETECTION.** 

You can make policies to block known malicious behaviors automatically. 

Manual response gives a wide range of response capabilities.

**SOME MANUAL RESPONSES:**

- **Isolate Host**

During any malicious activity on an endpoint, you can isolate that endpoint from the network through EDR.
This is a very effective function for containing malicious activity because most attacks start from a single endpoint and move laterally to other endpoints to compromise the whole network.

- **Terminate Process**
  
Not every malicious activity requires host isolation for instance hosts that run the core business operations. Isolating them can cause more loss than the malicious activity. 
In such cases, terminating a process within the EDR option is enough to neutralize the malicious activity. 
They can terminate any process at any time but this action should be taken consciously since terminating a legitimate process can disrupt the endpoint.


- **Quarantine**
  
If a malicious file comes into the endpoint, it can be quarantined. 
This ensures that the file is moved to an isolated location where it can not be executed so that the analysts can first review the file to restore or permanently remove it. 

- **Remote Access**


Analysts can  remotely access the shell of any endpoint when the EDR's built-in response is not enough to take action on a specific activity. 
By this, they gain deeper visibility into the system or take custom actions within the endpoints and also run scripts or collect  desired data from the host.
Below is an example of CrowdStrike Falcon EDR's RTR (Real Time Response) console, which allows analysts to remotely access the shell of any endpoint and run commands and scripts.
CrowdStrike Falcon EDR's RTR (Real Time Response) console.

<img width="1365" height="613" alt="image" src="https://github.com/user-attachments/assets/b574104c-f885-4dbb-9452-f92b134820ca" />


- **Artifacts Collection**

Sometimes, the analysts may need to extract some data from the endpoints for detailed forensic investigation or reporting for legal actions. 

This can be done from the endpoints without physically accessing the device. 

The most commonly extracted artefacts include:
  - Memory Dump
  - Event Logs
  - Specific Folder Contents
  - Registry Hives

---

## Pactical: INVESTIGATING AN ALERT ON EDR

**SCENARIO:**

You are a SOC analyst at TECH THM with access to the EDR console, having multiple medium and high-severity detections. 

Your task is to perform triage on each detection using the available information in the EDR and answer a series of questions related to these detections. 

<img width="1351" height="636" alt="image" src="https://github.com/user-attachments/assets/e643332a-f10f-4809-ba7c-4015f54aa3a7" />


1. Which tool was launched by CMD.exe to download the payload on DESKTOP-HR01? CURL.exe

<img width="1351" height="639" alt="image" src="https://github.com/user-attachments/assets/39ebb3e6-4c58-4190-ac3b-a57297109d88" />

2. What is the absolute path to the downloaded malware on the DESKTOP-HR01 machine?

   Downloaded file saved in the puclic folder. Hence path:

<img width="1357" height="614" alt="image" src="https://github.com/user-attachments/assets/31b324ed-ba32-44d2-86fe-06c4a8c7c306" />



4. What is the absolute path to the suspicious syncsvc.exe on the WIN-ENG-LAPTOP03 machine?

   C:\Users\haris.khan\AppData\Local\Temp\syncsvc.exe

<img width="1352" height="605" alt="image" src="https://github.com/user-attachments/assets/1ace3451-6f09-42e2-835d-5f96dc7b5924" />

5. On which URL was the exfiltration attempt being made on WIN-ENG-LAPTOP03?

When investigating the detection on WIN-ENG-LAPTOP03, the EDR console flagged a suspicious process — syncsvc.exe — located in the Temp directory. This tool was used for credential dumping via LSASS memory access, which created a dump file (dump_2025.dmp).

But the most critical finding came from the Network Activity section in the process details. As highlighted in the screenshot below, the EDR recorded that syncsvc.exe attempted to exfiltrate the dump file to an external server:

Attempted exfil to:
https://files-wetransfer.com/upload/session/ab12cd34ef56/dump_2025.dmp

<img width="1323" height="625" alt="image" src="https://github.com/user-attachments/assets/e5e1899d-1a14-4171-9cd3-53bdafd7b8d9" />

6. What was UpdateAgent.exe labelled by Threat Intel on DESKTOP-DEV01? Known internal IT utility tool

<img width="1353" height="632" alt="image" src="https://github.com/user-attachments/assets/f16b86c8-23fd-4ad7-9e59-804df759568d" />

<img width="1325" height="558" alt="image" src="https://github.com/user-attachments/assets/353ec107-b714-4f6c-9161-f83d69de0dba" />






