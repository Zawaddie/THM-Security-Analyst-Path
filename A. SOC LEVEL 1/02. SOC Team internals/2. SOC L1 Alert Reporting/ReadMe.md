# SOC L1 Alert Reporting

During or after alert triage, L1 analysts may be uncertain about how to classify the alert, requiring senior support or information from the system owner. Also, L1 may deal with real cyberattacks and breaches that need immediate attention and remediation actions. 
This room covers these cases by introducing three new terms: alert reporting, escalation, and communication.

## My TakeHomes from the Room

First, L1 analysts receive the alerts in a SIEM, EDR, or a ticket management platform. 

Most of the alerts are closed as **False Positives** or are handled on L1 level, but complex and threatening ones are sent to L2 that remediate most breaches. 

To send the alerts further, needs to learn: 
- **Reporting**: Before closing or passing the alert to L2, you might have to report it.
  Depending on team standards and alert severity, instead of a short alert comment, you can be required to document your investigation in detail, ensuring all relevant evidence is included.
  This is especially important for True Positives, which require escalation.
- **Alert Escalation**: If the True Positive alert requires additional actions or deeper investigation, escalate it to the L2 analyst for further review following the agreed procedures.
  That's where your alert report comes in handy since L2 will use it to get the initial context and spend less on the analysis from scratch.
- **Communication**: You may also need to communicate with other departments during or after the analysis.
  For example, ask the IT team if they confirm granting administrative privileges to some users or contact HR to get more information about the newly hired employee.

**Having L1 analysts write alert reports serves several key purposes:**

<img width="992" height="317" alt="image" src="https://github.com/user-attachments/assets/6f9bb3d4-a3a9-4ee7-a146-c94367f0eeea" />

Recommended to follow the [Five Ws approach](https://en.wikipedia.org/wiki/Five_Ws) and include at least these items in the report:

- **Who:** Which user logs in, runs the command, or downloads the file
- **What:** What exact action or event sequence was performed
- **When:** When exactly did the suspicious activity start and ended
- **Where:** Which device, IP, or website was involved in the alert
- **Why:** The most important W, the reasoning for your final verdict

<img width="1327" height="590" alt="image" src="https://github.com/user-attachments/assets/d4f06a01-84f0-48ed-88df-6b3c0f312bad" />





