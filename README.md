# Active Directory SOC Home Lab

🚧 **Status: Work in Progress**

A hands-on cybersecurity home lab designed to simulate an enterprise Windows environment and build practical SOC analyst skills through Active Directory administration, endpoint management, security monitoring, and threat detection.

---

## Project Overview

This project focuses on building an enterprise-style lab environment from the ground up.

The current phase covers:

- Windows Server deployment
- Active Directory Domain Services (AD DS)
- DNS configuration
- User and access management
- Organizational Units (OUs)
- Group Policy security controls
- Windows endpoint domain integration

Future phases will expand this environment into a complete SOC simulation with SIEM monitoring, attack simulations, and detection engineering.

---

# Lab Architecture

```
                    cyberlab.local
                          |
                          |
              Windows Server 2025 (DC01)
                    Domain Controller
                          |
              -------------------------
                          |
              Windows 11 Pro (Client01)
                  Domain Joined Endpoint
```

---

# Technologies Used

### Infrastructure

- Windows Server 2025 (Server Core)
- Windows 11 Pro
- Oracle VirtualBox

### Active Directory

- Active Directory Domain Services (AD DS)
- DNS
- PowerShell Administration
- User Management
- Organizational Units
- Group Policy Objects (GPO)

### Security Operations (Upcoming)

- Splunk Enterprise
- Sysmon
- Windows Event Monitoring
- SIEM Analysis
- MITRE ATT&CK Mapping
- Attack Simulation
- Detection Engineering

---

# Completed Work

## ✅ Active Directory Deployment

Built and configured a Windows domain environment:

- Installed Active Directory Domain Services
- Promoted Windows Server to Domain Controller
- Created `cyberlab.local` domain
- Configured DNS services
- Verified Domain Controller functionality

![Domain Controller](images/dc01-domain-controller.png)

---

## ✅ Active Directory User Management

Created and managed domain users and organizational structure using Active Directory.

Implemented:

- User accounts
- Organizational Units
- Domain administration

![Domain Users](images/dc01-domain-users.png)

![Organizational Units](images/dc01-organizational-units.png)

---

## ✅ Windows Endpoint Integration

Joined a Windows 11 workstation to the Active Directory domain.

Verified:

- Domain membership
- Domain authentication
- Communication with Domain Controller

![Domain Membership](images/client01-domain-membership.png)

---

## ✅ Domain Authentication Verification

Validated successful authentication using domain credentials.

Example:

```
CYBERLAB\shreya.bista
```

Verification:

```cmd
whoami
```

![Domain Authentication](images/client01-domain-user-authentication.png)

---

## ✅ Network Configuration

Verified endpoint connectivity and Active Directory DNS configuration.

```cmd
ipconfig /all
```

![Network Configuration](images/client01-network-config.png)

---

# Security Skills Demonstrated

This project demonstrates practical experience with:

✅ Windows Server Administration  
✅ Active Directory Management  
✅ Identity and Access Management  
✅ PowerShell Administration  
✅ Domain Authentication  
✅ Group Policy Configuration  
✅ Endpoint Management  
✅ Cybersecurity Lab Development  

---

# Future Development Roadmap

## SOC Monitoring Environment

Planned additions:

- [ ] Configure advanced Windows auditing
- [ ] Deploy Sysmon
- [ ] Forward Windows security logs
- [ ] Integrate Splunk SIEM
- [ ] Create detection rules
- [ ] Simulate attacks
- [ ] Investigate security incidents
- [ ] Map detections to MITRE ATT&CK techniques

---

# Related Projects

Other cybersecurity projects:

- Microsoft Sentinel Failed Login Detection Lab
- Splunk Windows Authentication Monitoring Lab
- Python Security Log Analyzer
- Wireshark Malware Traffic Analysis

---

# About Me

**Shreya Bista**

Cybersecurity Graduate | CompTIA Security+ Certified

Interested in Security Operations, Threat Detection, and Defensive Security Engineering.
