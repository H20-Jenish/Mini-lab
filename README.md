## <img width="607" height="420" alt="Mini_Detection Lab" src="https://github.com/user-attachments/assets/758bdf53-eafe-42be-8890-58bba9d7a4c7" />
📖 Overview

This virtual environment is a purpose-built home laboratory designed for simulating cyberattacks, monitoring network traffic, and practicing Digital Forensics and Incident Response (DFIR). The lab utilizes a **pfSense** firewall to segment the network into distinct security zones, mirroring a real-world enterprise architecture.

## 🏗️ Network Architecture

The lab is centered around a **pfSense 2.8.1** router/firewall, which manages traffic between five distinct segments:

|**Zone**|**Description**|**Key Assets**|
|---|---|---|
|**WAN**|External network (Internet)|Kali Linux (Attacker)|
|**ADMIN_ZONE**|Management & Administrative tasks|Windows 10 Pro|
|**DMZ_ZONE**|Public-facing services|Windows IIS Server 2K22 (`banking.rudrait.net`)|
|**LOCAL_ZONE**|Vulnerable internal resources|Metasploitable 2|
|**SOC_ZONE**|Security monitoring and IR tools|Wazuh Server, DFIR-IRIS|

---
## 💻 Component Breakdown

### 1. The Attacker (Kali Linux)
Located outside the network (connected via NAT - VMnet 8), this machine simulates external threats attempting to breach the DMZ or pivot into the internal network.
### 2. The Targets
- **Windows IIS Server 2022:** A modern Windows target hosting an ASPX web application (`banking.rudrait.net`). This is ideal for testing SQLi, XSS, and web-shell uploads.
- **Metasploitable 2:** A "low-hanging fruit" Linux target used for practicing network exploitation and lateral movement.
### 3. The Defensive Stack (SOC_ZONE)
- **Wazuh 4.14.3:** Acts as the SIEM/XDR, collecting logs and monitoring host integrity across all zones.
- **DFIR-IRIS:** A professional-grade incident response platform used for case management.
- **Integration:** Wazuh is configured to push alerts directly to IRIS, creating a seamless "Alert-to-Ticket" workflow.
---
## 🛠️ Key Capabilities

- **Traffic Analysis:** Monitor how pfSense handles traffic between different subnets.
- **Web App Security:** Test vulnerabilities on the custom `.aspx` banking application.
- **EDR/XDR Practice:** Install Wazuh agents on the Windows and Linux targets to detect real-time exploitation.
- **Incident Management:** Practice the full IR lifecycle by tracking investigations within DFIR-IRIS.
---
## 👁️ Lab Analysis

This setup is highly effective for a "mini" lab because it focuses on **modern workflows** rather than just old-school exploitation.
### What makes this lab great :

- **Segmented Reality:** Many labs put everything on one flat subnet. By using pfSense to create an `ADMIN_ZONE` and a `DMZ_ZONE`, you are forced to learn about firewall rules and how attackers "pivot" between segments.
- **The IRIS Integration:** This is the "secret sauce" of your lab. Integrating Wazuh with IRIS elevates this from a "hacking lab" to a "Security Operations lab." It teaches you how to manage a high volume of alerts and organize forensic evidence.
- **The IIS Target:** Hosting a specific `.aspx` app on Windows Server 2022 is a much more realistic scenario for corporate environments than just attacking Metasploitable.
