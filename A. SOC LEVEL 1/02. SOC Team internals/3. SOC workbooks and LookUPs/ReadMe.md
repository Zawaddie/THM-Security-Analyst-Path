# SOC Workbooks and LookUPs
Alert triage is a complex process that often requires analysts to gather additional information about affected employees or servers. 

SOC workbooks designed to streamline alert triage and explains various lookup methods to quickly retrieve user and system context.

## My TakeHomes from the room:

**Identity inventory:**

A catalogue of corporate employees (user accounts), services (machine accounts), and their details like privileges, contacts, and roles within the company.

**Asset inventory:**

Also called asset lookup.

Is a list of all computing resources within an organisation's IT environment. 

Note that while "asset" is a vague term and can also refer to software, hardware, or employees, this room emphasises servers and workstations only. 

**Network Diagrams**

Network diagrams for the organization that you are protecting  helpd a great deal when you are working on alerts.

With asset inventory and network diagrams, you can get enough context about the user, host, or IP address

**SOC workbook**

Also called playbook, runbook, or workflow, 

It is a structured document that defines the steps required to investigate and remediate specific threats efficiently and consistently.

The workbook is divided into three logical groups. 
By following the steps in the correct order, you can guarantee high-quality alert triage and eliminate cases where the verdict is made without enough evidence:

- **Enrichment:** Use Threat Intelligence and identity inventory to get information about the affected user
- **Investigation:** Using the gathered data and SIEM logs, make your verdict if the login is expected
- **Escalation:** Escalate the alert to L2 or communicate the login with the user if necessary

  <img width="969" height="531" alt="image" src="https://github.com/user-attachments/assets/45c1212c-3b9c-4972-bc27-6ef721c35957" />

  






