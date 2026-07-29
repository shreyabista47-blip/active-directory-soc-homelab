# Active Directory SOC Home Lab

🚧 **Project Status: Work in Progress**

## Overview

This project documents the development of an enterprise-style cybersecurity home lab designed to simulate a real-world Windows domain environment.

The goal of this lab is to build hands-on experience with:

- Windows Server administration
- Active Directory management
- Group Policy configuration
- Endpoint management
- Security monitoring
- Threat detection
- Incident response

This environment will continue to evolve into a Security Operations Center (SOC) simulation with SIEM monitoring and attack detection.

---

# Lab Architecture

The current environment consists of:

| System | Role |
|---|---|
| DC01 | Windows Server 2025 Domain Controller |
| Client01 | Windows 11 Pro Domain-Joined Workstation |

---

# Technologies Used

## Infrastructure

- Windows Server 2025
- Windows 11 Pro
- Oracle VirtualBox

## Active Directory

- Active Directory Domain Services (AD DS)
- DNS
- Organizational Units
- User Management
- Group Policy Objects (GPO)

## Security Operations (Upcoming)

- Splunk Enterprise
- Sysmon
- Windows Event Logs
- MITRE ATT&CK Framework
- Attack Simulation
- Detection Engineering

---

# Completed Progress

## Phase 1: Active Directory Environment ✅

Completed:

- ✅ Virtual machine deployment
- ✅ Windows Server configuration
- ✅ Active Directory Domain Services installation
- ✅ Domain Controller deployment
- ✅ DNS configuration
- ✅ Active Directory user creation
- ✅ Organizational Unit creation
- ✅ Windows 11 domain joining
- ✅ Group Policy configuration

---

# Project Documentation

## Environment Setup

Lab architecture and virtual machine setup:

[Environment Setup](01-Environment-Setup/setup.md)

---

## Active Directory Configuration

Domain Controller setup, users, and organizational units:

[Active Directory Documentation](02-Active-Directory/active-directory.md)

---

## Domain Join

Windows client domain integration and authentication testing:

[Domain Join Documentation](03-Domain-Join/domain-join.md)

---

## Group Policy

Security policies and centralized management:

[Group Policy Documentation](04-Group-Policy/group-policy.md)

---

# Upcoming Development

## Phase 2: SOC Monitoring Environment ⏳

Planned additions:

- [ ] Enable advanced Windows auditing
- [ ] Deploy Sysmon
- [ ] Configure log collection
- [ ] Integrate Splunk Enterprise
- [ ] Monitor Windows authentication events
- [ ] Detect brute-force attacks
- [ ] Create detection rules
- [ ] Map activity to MITRE ATT&CK techniques
- [ ] Perform incident response investigations

---

# Current Skills Demonstrated

This project demonstrates practical experience with:

- Windows Server administration
- Active Directory deployment
- Domain management
- PowerShell administration
- User and access management
- Group Policy configuration
- Endpoint troubleshooting
- Security-focused lab development

---

# Author

**Shreya Bista**

Cybersecurity Graduate | Security+ Certified
