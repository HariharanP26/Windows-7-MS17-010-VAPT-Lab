# Windows 7 MS17-010 (EternalBlue) Vulnerability Assessment and Penetration Testing Lab

## Overview

This project demonstrates a complete Vulnerability Assessment and Penetration Testing (VAPT) workflow performed against a vulnerable Windows 7 SP1 x64 machine in an isolated and authorized virtual lab environment.

The assessment includes reconnaissance, service enumeration, SMB enumeration, vulnerability validation, exploitation, post-exploitation verification, and remediation recommendations.

> **Disclaimer:** This project was conducted in a controlled lab environment for educational purposes only. No unauthorized systems were targeted.

---

# Objectives

- Discover live hosts
- Perform port and service enumeration
- Enumerate SMB shares
- Identify vulnerable services
- Validate the MS17-010 (EternalBlue) vulnerability
- Demonstrate successful exploitation in an authorized lab
- Perform basic post-exploitation enumeration
- Document remediation recommendations

---

# Lab Environment

| Component | Details |
|-----------|---------|
| Attacker Machine | Kali Linux |
| Target Machine | Windows 7 SP1 x64 |
| Network | VirtualBox Host-Only Network |
| Target IP | 192.168.100.5 |
| Framework | Metasploit Framework |
| Purpose | Authorized Security Testing Lab |

---

# Tools Used

- Nmap
- NSE (Nmap Scripting Engine)
- smbclient
- enum4linux
- Metasploit Framework
- Meterpreter

---

# Assessment Methodology

## 1. Reconnaissance

Performed initial host discovery and network reconnaissance.

### Commands Used

```bash
nmap -sV -p- 192.168.100.5
```

### Result

- Host is alive
- Windows operating system detected
- Multiple Microsoft RPC services identified

---

## 2. Port Scanning

Identified open ports and running services.

### Open Ports

| Port | Service |
|-------|----------|
|135|MSRPC|
|139|NetBIOS|
|445|SMB|
|49152-49157|Microsoft RPC|

### Screenshot

```
screenshots/01-nmap-service-scan.png
```

---

## 3. SMB Enumeration

Enumerated SMB shares using multiple tools.

### Commands

```bash
nmap --script smb-enum-shares -p445 192.168.100.5

smbclient -L \\\\192.168.100.5 -N

enum4linux -a 192.168.100.5
```

### Shares Discovered

- ADMIN$
- C$
- IPC$

### Information Collected

- Computer Name
- Workgroup
- SMB Service
- NetBIOS Information
- Windows Version

### Screenshots

```
screenshots/02-smb-enum.png

screenshots/03-smbclient.png

screenshots/04-enum4linux.png
```

---

## 4. Vulnerability Assessment

Validated SMB-related vulnerabilities using Nmap NSE scripts.

### Command

```bash
nmap --script smb-vuln* -p445 192.168.100.5
```

### Finding

The target was identified as vulnerable to:

- MS17-010
- CVE-2017-0144
- EternalBlue

### Risk Level

Critical

### Screenshot

```
screenshots/05-ms17-vulnerability.png
```

---

## 5. Exploitation (Authorized Lab)

The identified vulnerability was validated using the Metasploit Framework within the authorized lab environment.

### Metasploit Module

```
exploit/windows/smb/ms17_010_eternalblue
```

### Activities

- Verified target compatibility
- Loaded exploitation module
- Configured payload
- Established Meterpreter session

### Screenshots

```
screenshots/06-metasploit-search.png

screenshots/07-module-options.png

screenshots/08-running-exploit.png
```

---

## 6. Post-Exploitation

After successful exploitation, basic host validation was performed.

### Information Collected

- Operating System
- Architecture
- Computer Name
- Logged-in Users
- Directory Structure

### Example

```
Windows 7 SP1 x64

Computer Name:
WIN-845Q99004PP

Architecture:
64-bit

Directory Listing:
C:\
```

### Screenshot

```
screenshots/09-meterpreter-session.png
```

---

# Findings

| Severity | Finding |
|----------|----------|
| Critical | MS17-010 (EternalBlue) |
| High | SMBv1 Enabled |
| Medium | SMB Shares Exposed |
| Low | Information Disclosure through SMB Enumeration |

---

# Remediation Recommendations

- Apply Microsoft MS17-010 security updates.
- Disable SMBv1.
- Restrict SMB access using firewall rules.
- Enable network segmentation.
- Apply the principle of least privilege.
- Perform regular vulnerability assessments.
- Deploy Endpoint Detection and Response (EDR).
- Monitor SMB activity through centralized logging.

---

# Skills Demonstrated

- Network Reconnaissance
- Service Enumeration
- SMB Enumeration
- Vulnerability Assessment
- CVE Validation
- Metasploit Framework
- Meterpreter
- Windows Enumeration
- Post-Exploitation Analysis
- Security Reporting

---

# Project Structure

```
Windows-7-MS17-010-VAPT-Lab/

│── README.md

│── screenshots/
│   ├── 01-nmap-service-scan.png
│   ├── 02-smb-enum.png
│   ├── 03-smbclient.png
│   ├── 04-enum4linux.png
│   ├── 05-ms17-vulnerability.png
│   ├── 06-metasploit-search.png
│   ├── 07-module-options.png
│   ├── 08-running-exploit.png
│   └── 09-meterpreter-session.png

│── reports/
│   ├── reconnaissance.md
│   ├── enumeration.md
│   ├── vulnerability-assessment.md
│   ├── post-exploitation.md
│   └── remediation.md
```

---

# Key Takeaways

- Successfully identified exposed SMB services.
- Enumerated SMB shares and system information.
- Verified the presence of the MS17-010 (EternalBlue) vulnerability.
- Demonstrated exploitation in a controlled lab environment.
- Performed post-exploitation validation using Meterpreter.
- Documented findings and remediation recommendations following VAPT methodology.

---

## Author

**Hari Haran**

Cybersecurity Enthusiast | VAPT | Penetration Testing | Network Security | Linux | Windows Security

---

## License

This repository is intended for educational purposes only.

The techniques demonstrated were performed exclusively within an isolated, authorized laboratory environment.
