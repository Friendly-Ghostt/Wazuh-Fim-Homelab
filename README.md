# File Integrity Monitoring (FIM) with Wazuh

![Wazuh Logo](https://upload.wikimedia.org/wikipedia/commons/1/17/Wazuh_logo.png)

## Project Overview

This project demonstrates the deployment of **Wazuh for File Integrity Monitoring (FIM)** in a **homelab environment**. It monitors critical system files, detects unauthorized changes, and generates real-time security alerts.

FIM is essential for detecting:
- Unauthorized file modifications  
- Suspicious changes in configuration files  
- Potential malware or intrusion activity  

This project integrates **Wazuh Manager**, **Wazuh Indexer**, **Wazuh Agent**, and **Wazuh Dashboard** on Linux and Windows systems to simulate a real SOC workflow.

---

## Architecture
[Ubuntu Server / Windows Agent] --> [Wazuh Manager (Ubuntu)] --> [Wazuh Dashboard]

---


**Components:**
- **Wazuh Manager (Ubuntu)** – Central server collecting logs and running FIM rules.  
- **Wazuh Agent** – Installed on target systems to monitor files and directories.  
- **Wazuh Dashboard** – Web interface for alerts visualization and reporting.  

---

## Project Objectives

1. Implement **File Integrity Monitoring** using Wazuh.  
2. Configure **syscheck** rules to monitor key directories.  
3. Test alerting by performing controlled file modifications.  
4. Document the process with screenshots, logs, and configurations.  
5. Showcase detection and alerting in Wazuh Dashboard.  

---

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| Wazuh Manager | Central FIM and SIEM server |
| Wazuh Agent | Monitors file changes on endpoints |
| Wazuh Dashboard | Visualize alerts and events |
| Ubuntu Server | Host for Wazuh Manager |
| Windows Server | Agent target system |
| VirtualBox / VMware | Homelab virtualization environment |

---

## Installation & Setup

### 1. Wazuh Manager (Ubuntu)

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Add Wazuh repository and install manager
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
sudo apt update
sudo apt install wazuh-manager -y
# Start manager
sudo systemctl enable wazuh-manager
sudo systemctl start wazuh-manager
```
---
### 2. Wazuh Agent (Windows)
- Install agent on target machines
- Configure agent to connect to Wazuh Manager IP
- Start agent service
  
 ### 3. Wazuh Indexer
```bash
# Install Wazuh Indexer on Ubuntu
sudo apt install wazuh-indexer -y
sudo systemctl enable wazuh-indexer
sudo systemctl start wazuh-indexer
```
---
### 4. Wazuh Dashboard
```bash
# Install Wazuh Dashboard on Ubuntu
sudo apt install wazuh-dashboard -y
sudo systemctl enable wazuh-dashboard
sudo systemctl start wazuh-dashboard
```
- Access via https://10.0.0.122:5601
---
## FIM Configuration
#### File integrity monitoring is configured in ossec.conf under <syscheck>:
```xml
<syscheck>
  <directories check_all="yes">Desired Directories</directories>
  <frequency>60</frequency>
  <alert_new_files>yes</alert_new_files>
</syscheck>
```
---
## Testing & Validation
- Modify a monitored file/Directory
- Wait for syscheck scan (or restart manager with sudo systemctl restart wazuh-manager).
- Check Wazuh Dashboard for alerts under File Integrity Monitoring.
---
## Project Outcome
- Successfully deployed Wazuh FIM in a homelab environment
- Detected and logged file changes on Linux and Windows endpoints
- Demonstrated real-time alerting and visualization in Wazuh Dashboard
- Prepared a professional, reproducible setup for SOC demonstration
---
## License
This project is for **educational and lab purposes only.** Do not use tools like Hydra against systems you do not own or have explicit permission to test.
