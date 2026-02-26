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









