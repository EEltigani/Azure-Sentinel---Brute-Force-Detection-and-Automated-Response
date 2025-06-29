🚨 Microsoft Sentinel - Brute Force Detection & Automation

This project demonstrates the implementation of a custom security detection and automation rule in Microsoft Sentinel to identify and respond to multiple brute-force login attempts on an Azure-hosted VM. The solution includes analytics rule creation, alerting, incident automation, and mitigation using real data and simulated attacks.
📌 Project Overview

This project showcases:

- Real-time detection of Event ID 4625 (failed logins)

- Identification of multiple login attempts from the same IP address

- Automation of incident responses for known false positives

- Entity mapping, incident ownership assignment, and status updates

- Integration with MITRE ATT&CK (Credential Access)

The implementation is based on a combination of KQL queries, Sentinel analytics rules, and automation rules with logic conditions to auto-resolve benign activity.

📂 Features

✅ Custom KQL analytics rule
✅ Alert on repeated failed login attempts (Event ID 4625)
✅ Query logic to catch brute-force activity
✅ Entity mapping (Account, IP, Hostname)
✅ Automation rule to auto-close alerts from test accounts
✅ Incident assigned to analyst automatically
✅ Severity labelling (Low, Medium, High)
✅ Full evidence capture and timeline

⚙️ Technologies Used

- Microsoft Sentinel

- Log Analytics / Kusto Query Language (KQL)

- Azure VM

- Analytics Rules

- Automation Rules

- Entity Behaviour Mapping

- MITRE ATT&CK Mapping

🧪 Query Logic (KQL)

SecurityEvent
| where EventID == 4625 and TimeGenerated > ago(5m)
| summarize count() by IpAddress, Account, Computer
| where count_ > 3

This rule counts failed login attempts (Event ID 4625) grouped by IP, Account, and Computer in a 5-minute window. If more than 3 attempts are detected from the same source, an alert is raised.

🧠 Automation Rule Logic

Trigger: When an incident is created
Conditions:

- Incident provider equals Microsoft Sentinel

- Analytic rule name contains Multiple Login Attempts

- Account name equals -\Vagrant, -\Named, -\Pos, etc.
  Actions:
  Change status to Closed
  Assign reason: Benign Positive - Suspicious but expected
  Assign owner: Analyst (You)

  🖼️ Screenshots

All screenshots of the rule creation, logs, and automation configuration are available in the attached Word document: Sentinel Screenshots.

👤 Author

Emad Eltigani
Microsoft Sentinel Security Analyst (Lab Project)

- Successfully built and automated real-time brute-force attack detection.

✅ Status

🟢 Complete – All incidents are correctly triggering, auto-closing for false positives, and assigning ownership as intended.

📽️ Reference Tutorials

JoshMadakor: https://www.youtube.com/watch?v=g5JL2RIbThM&t=3259s&ab_channel=JoshMadakor
ProHut: https://www.youtube.com/watch?v=fcMwmd3bSdk&ab_channel=ProHut
