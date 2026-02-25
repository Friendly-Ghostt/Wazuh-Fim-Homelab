# Wazuh SIEM & File Integrity Monitoring Homelab

## 📌 Project Overview
Deployed and configured Wazuh SIEM on Ubuntu Server in a virtualized homelab environment. Implemented File Integrity Monitoring (FIM) to detect unauthorized file creation, modification, and deletion events from a Windows Server agent.

---

## 🖥 Lab Environment
- Host Machine: Windows 11 (16GB RAM)
- VM1: Ubuntu Server 22.04 – Wazuh Manager
- VM2: Windows Server 2025 – Wazuh Agent
- Network Mode: Bridged
- Communication Port: 1514/TCP

---

## ⚙ Configuration

Enabled File Integrity Monitoring by editing:

`/var/ossec/etc/ossec.conf`

Configured:
- `<syscheck>` enabled
- Scan frequency set to 60 seconds
- Monitored directories:
  - /home (Linux)
  - C:\Users (Windows)

---

## 🔎 Testing & Validation
- Created test file → Alert generated
- Modified file → Hash change detected
- Deleted file → Deletion alert observed
- Verified agent connectivity in dashboard

---

## 🚧 Challenges & Troubleshooting
- TCP connection failure between agent and manager
- Firewall blocking port 1514
- Incorrect monitored directory path
- Default FIM frequency too high (12 hours)

Resolved through:
- Network troubleshooting
- Service restarts
- Configuration updates

---

## 🧠 Skills Demonstrated
- SIEM Deployment
- Linux Administration
- Windows Server Management
- Log Analysis
- Network Troubleshooting
- Security Monitoring
