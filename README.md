# SOC Home Lab

## 🎯 Objective
Build a self-hosted SOC (Security Operations Center) home lab to demonstrate foundational skills in threat detection, log forwarding, and SIEM analysis using Splunk and multiple operating systems.

---

## 🛠️ Tools & Technologies Used
- **Splunk Enterprise (SIEM)**
- **Windows Server 2019** (Event log source)
- **Ubuntu Server** (Syslog source)
- **Kali Linux** (Attack simulation with Hydra)
- **Ubuntu Desktop** (Splunk installed here)
- **VirtualBox** (VM Management)
- **Winlogbeat**, **Sysmon**, **rsyslog**

---

## 🧪 Lab Structure
SOC-Home-Lab/
│
├── config/ # Configuration files (Winlogbeat, Sysmon, rsyslog)
├── dashboards/ # Splunk dashboard exports (XML)
├── detections/ # SPL queries used to detect attacks
├── reports/ # Lab summary and attack documentation
└── README.md # This file

---

## 🔍 Activities Completed

### ✅ 1. Virtual Environment Setup
- Created 4 Virtual Machines using VirtualBox:
  - Ubuntu Desktop (Splunk)
  - Ubuntu Server (Log source)
  - Windows Server 2019 (Log source)
  - Kali Linux (Attack simulator)

### ✅ 2. Log Forwarding Configuration
- Windows logs collected using **Winlogbeat** and enriched with **Sysmon**
- Ubuntu Server logs sent using **rsyslog**
- Logs forwarded to Splunk via port `9997` (TCP) and `514` (UDP)

### ✅ 3. Attack Simulation
- Simulated a brute-force SSH attack from Kali Linux using Hydra

### ✅ 4. Detection in Splunk
- Ran SPL query to detect multiple failed SSH login attempts:
```spl
index=* sourcetype=syslog "Failed password"
| stats count by host, user, src
| where count > 5

✅ 5. Dashboard
Created Splunk dashboard visualizing brute-force SSH detection

Exported dashboard to dashboards/brute_force_dashboard.xml

📁 Files You Can Check
dashboards/brute_force_dashboard.xml: The main Splunk dashboard export

detections/: SPL query used for brute-force detection

config/: Config files for rsyslog, Winlogbeat, and Sysmon (to be added)

reports/: Will contain documentation and IR playbooks

🧠 Outcome
This project demonstrates real-world SOC analyst skills, from environment setup to attack detection using open-source tools and enterprise SIEM.

