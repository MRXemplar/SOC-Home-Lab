# SOC Home Lab

## 🎯 Objective
Build a self-hosted SOC (Security Operations Center) home lab to demonstrate key cybersecurity skills including threat detection, log forwarding, and SIEM analysis using Splunk.

---

## 🛠️ Tools & Technologies
- **Splunk Enterprise** – SIEM tool
- **Windows Server 2019** – Windows event log source
- **Ubuntu Server** – Syslog source
- **Kali Linux** – Attack simulation
- **Ubuntu Desktop** – Splunk installed here
- **VirtualBox** – VM management
- **Winlogbeat** + **Sysmon** – Windows log forwarding & enrichment
- **rsyslog** – Linux log forwarding

---

## 🧪 Lab Architecture

```
SOC-Home-Lab/
├── config/               # Configuration files (Sysmon, Winlogbeat, rsyslog)
├── dashboards/           # Splunk dashboard exports
├── detections/           # SPL queries for threat detection
├── reports/              # Documentation and findings
└── README.md             # Project overview
```

---

## ✅ Lab Setup Summary

### 🔧 1. Virtual Machines Created
- **Ubuntu Desktop**: Splunk installed and running
- **Windows Server 2019**: Used as a Windows event log source
- **Ubuntu Server**: Used as a Linux syslog source
- **Kali Linux**: Used to simulate attacks (Hydra SSH brute-force)

### 🔌 2. Log Forwarding Configured
- **Windows**: 
  - Installed Sysmon for advanced log collection
  - Installed and configured Winlogbeat to forward logs to Splunk
- **Ubuntu Server**:
  - Configured rsyslog to forward system logs via UDP/514
- **Splunk**:
  - Enabled data input for TCP/9997 and UDP/514
  - Confirmed receipt of logs from both Windows and Ubuntu

### ⚔️ 3. Attack Simulated
- Used Hydra from Kali Linux to simulate a brute-force SSH attack:
  ```bash
  hydra -l test -P /usr/share/wordlists/rockyou.txt ssh://<target-ip>
  ```

### 🔍 4. Detection Performed in Splunk
- Verified logs in Splunk and created a basic SPL query to detect brute-force attempts:
  ```spl
  index=* sourcetype=syslog "Failed password"
  | stats count by host, user, src
  | where count > 5
  ```
- Exported dashboard visualizing brute-force activity

---

## 📁 Key Files

| Path | Description |
|------|-------------|
| `dashboards/brute_force_dashboard.xml` | Splunk dashboard export (XML) showing failed SSH login detections |
| `detections/ssh_brute_force_query.spl` | SPL query used to detect SSH brute-force attacks |
| `config/` | Placeholder for Winlogbeat, Sysmon, and rsyslog config files (to be added) |

---

## 🔜 Next Steps
> These are planned but **not included** in the project yet:

- Create Splunk alerts for automatic brute-force detection
- Add more attack simulations (e.g., malware, web defacement, lateral movement)
- Create and document incident response playbooks
- Upload full documentation and screenshots to `reports/`

---

## 🧠 Outcome
This lab demonstrates practical experience in:
- Setting up a real-world SOC environment
- Collecting logs from multiple operating systems
- Detecting and visualizing cyberattacks using Splunk
