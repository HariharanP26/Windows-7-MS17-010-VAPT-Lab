# 🛡️ Windows 7 MS17-010 (EternalBlue) Vulnerability Assessment & Penetration Testing Lab

<p align="center">

![Platform](https://img.shields.io/badge/Platform-Windows%207-blue)
![OS](https://img.shields.io/badge/Attacker-Kali%20Linux-success)
![Vulnerability](https://img.shields.io/badge/CVE-CVE--2017--0144-red)
![Severity](https://img.shields.io/badge/Severity-Critical-red)
![Framework](https://img.shields.io/badge/Framework-Metasploit-orange)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)
![License](https://img.shields.io/badge/License-Educational-lightgrey)

</p>

---

# 📖 Project Overview

This project demonstrates a **complete Vulnerability Assessment and Penetration Testing (VAPT)** engagement performed against a vulnerable **Windows 7 SP1 x64** machine within an isolated and authorized virtual lab environment.

The assessment follows a structured penetration testing methodology, including reconnaissance, enumeration, vulnerability validation, controlled exploitation, post-exploitation verification, and remediation planning.

The primary objective was to identify and validate the **MS17-010 (EternalBlue)** vulnerability while documenting each phase of the engagement in a professional manner.

> **⚠️ Disclaimer**
>
> This project was conducted exclusively in an isolated lab environment for educational and defensive security purposes. No unauthorized systems were targeted.

---

# 🎯 Objectives

✔ Discover the target host

✔ Enumerate exposed services

✔ Perform SMB enumeration

✔ Identify security weaknesses

✔ Validate MS17-010 vulnerability

✔ Demonstrate exploitation in an authorized lab

✔ Perform post-exploitation verification

✔ Recommend security mitigations

---

# 🖥️ Lab Architecture

```
                 VirtualBox Host-Only Network

+---------------------------------------------------------+

        Kali Linux                     Windows 7 SP1
      (Attacker VM)                  (Target Machine)

      192.168.100.3  ─────────────► 192.168.100.5

+---------------------------------------------------------+
```

---

# 🧰 Tools & Technologies

| Category | Tools |
|------------|-------------------------|
| Operating System | Kali Linux |
| Target | Windows 7 SP1 x64 |
| Network Scanner | Nmap |
| SMB Enumeration | smbclient |
| Enumeration | enum4linux |
| Vulnerability Detection | Nmap NSE Scripts |
| Exploitation | Metasploit Framework |
| Post Exploitation | Meterpreter |

---

# 🔄 VAPT Methodology

```
Reconnaissance
        │
        ▼
Port Scanning
        │
        ▼
Service Enumeration
        │
        ▼
SMB Enumeration
        │
        ▼
Vulnerability Assessment
        │
        ▼
Vulnerability Validation
        │
        ▼
Controlled Exploitation
        │
        ▼
Post Exploitation
        │
        ▼
Documentation & Remediation
```

---

# 🔍 Phase 1 — Reconnaissance

The assessment began by identifying live hosts and exposed network services.

### Activities

- Host Discovery
- Service Detection
- Version Detection
- Operating System Fingerprinting

### Tools

- Nmap

### Screenshot

```
screenshots/01-nmap-service-scan.png
```

---

# 🌐 Phase 2 — Port & Service Enumeration

Open ports were identified to determine the attack surface.

| Port | Service | Description |
|------|----------|-------------|
|135|MSRPC|Microsoft Remote Procedure Call|
|139|NetBIOS|NetBIOS Session Service|
|445|SMB|Server Message Block|
|49152-49157|RPC|Dynamic RPC Services|

---

# 📂 Phase 3 — SMB Enumeration

SMB enumeration was performed to identify accessible shares and gather system information.

### Enumeration Tools

- Nmap NSE
- smbclient
- enum4linux

### Information Collected

- Workgroup Name
- NetBIOS Information
- Computer Name
- SMB Shares
- SMB Version
- Windows Build Information

### Shares Identified

- ADMIN$
- C$
- IPC$

### Screenshots

```
Screenshots/02-smb-enum.png

Screenshots/03-smbclient.png

Screenshots/04-enum4linux.png
```

---

# 🚨 Phase 4 — Vulnerability Assessment

Nmap NSE scripts were used to validate known SMB vulnerabilities.

### Vulnerability Identified

| Vulnerability | Value |
|--------------|-------|
| CVE | CVE-2017-0144 |
| Microsoft Bulletin | MS17-010 |
| Common Name | EternalBlue |
| Severity | Critical |
| CVSS | 9.8 |

### Screenshot

```
Screenshots/05-ms17-vulnerability.png
```

---

# 💥 Phase 5 — Vulnerability Validation

The vulnerability was validated using the Metasploit Framework within the authorized lab environment.

### Framework

Metasploit

### Module

```
exploit/windows/smb/ms17_010_eternalblue
```

### Activities

- Module Selection
- Target Verification
- Payload Configuration
- Session Establishment

### Screenshots

```
Screenshots/06-metasploit-search.png

Screenshots/07-module-options.png

Screenshots/08-running-exploit.png
```

---

# 🖥️ Phase 6 — Post Exploitation

After successful exploitation, post-exploitation activities were conducted to validate access and collect basic system information.

### Information Gathered

- Operating System
- Computer Name
- Architecture
- Logged-in Users
- File System Structure

### Sample Output

```
Windows 7 SP1 x64

Architecture : x64

Computer Name : WIN-845Q99004PP

Directory Listing : C:\
```

### Screenshot

```
Screenshots/09-meterpreter-session.png
```

---

# 📊 Assessment Summary

| Category | Status |
|-----------|--------|
| Host Discovery | ✅ |
| Port Scanning | ✅ |
| SMB Enumeration | ✅ |
| Vulnerability Detection | ✅ |
| MS17-010 Validation | ✅ |
| Controlled Exploitation | ✅ |
| Post Exploitation | ✅ |
| Documentation | ✅ |

---

# 🚩 Key Findings

| Severity | Finding |
|-----------|----------|
| 🔴 Critical | MS17-010 (EternalBlue) |
| 🟠 High | SMBv1 Enabled |
| 🟡 Medium | SMB Information Disclosure |
| 🟢 Low | Default Administrative Shares Exposed |

---

# 🛡️ Remediation Recommendations

- Apply Microsoft MS17-010 Security Updates
- Disable SMBv1 Protocol
- Restrict SMB Access Through Firewalls
- Enable Network Segmentation
- Implement Principle of Least Privilege
- Deploy Endpoint Detection & Response (EDR)
- Perform Regular Vulnerability Assessments
- Monitor SMB Activity Using SIEM

---

# 🎓 Skills Demonstrated

- Vulnerability Assessment
- Penetration Testing
- Windows Security
- SMB Enumeration
- Network Reconnaissance
- Service Enumeration
- Nmap
- Metasploit Framework
- Meterpreter
- Post Exploitation
- Technical Documentation
- Security Reporting

---

# 📁 Repository Structure

```
Windows-7-MS17-010-VAPT-Lab/

├── README.md

├── Screenshots/

├── reports/

│   ├── reconnaissance.md

│   ├── enumeration.md

│   ├── vulnerability-assessment.md

│   ├── post-exploitation.md

│   └── remediation.md

└── LICENSE
```

---

# 📌 Key Takeaways

- Successfully identified exposed SMB services.
- Performed comprehensive SMB enumeration.
- Validated the MS17-010 (EternalBlue) vulnerability.
- Demonstrated controlled exploitation within an authorized lab.
- Conducted post-exploitation validation.
- Produced a professional security assessment with remediation recommendations.

---

# 👨‍💻 Author

**Hari Haran**

**Cybersecurity | VAPT | Penetration Testing | SOC | Network Security | Linux | Windows Security**

---

## ⭐ If you found this project useful, consider giving it a star!
