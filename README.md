# Active Directory SOC Home Lab

🚧 **Status: Work in Progress**

A hands-on cybersecurity home lab designed to simulate an enterprise Windows environment and develop practical SOC analyst skills through Active Directory administration, endpoint management, security monitoring, and threat detection.

---

# Project Overview

This project documents the development of an enterprise-style cybersecurity lab environment built from the ground up.

The goal is to gain practical experience with:

- Windows Server administration
- Active Directory management
- Identity and Access Management (IAM)
- Group Policy security controls
- Endpoint configuration
- Security monitoring
- Threat detection
- Incident response workflows

**The idea:** build a small but complete enterprise environment, then attack it on purpose, and use that attack to prove out a real detection pipeline, the same loop a SOC analyst lives in every day: an event happens, it gets logged, it gets collected, it gets investigated, and it gets turned into something that would catch the next one automatically.

**Phase 1** built the Windows enterprise foundation, Active Directory, a domain-joined endpoint, and centralized management via Group Policy. **Phase 2** turned that foundation into a working SOC detection environment: advanced audit logging, a simulated attacker, centralized log collection with Splunk, and detection engineering with alerting and a dashboard. Both phases are functionally complete, only one dashboard screenshot is still pending (noted below).

---

# Lab Architecture

                cyberlab.local
                      |
                      |
      Windows Server 2025 (DC01)
          Domain Controller
   AD DS + DNS + Advanced Audit Policy
                      |
                      |
      ---------------------------
      |                         |
      |                         |
Windows 11 Pro (Client01)      Kali Linux
 Domain Joined Endpoint      Attacker/Testing VM
- Splunk Universal Forwarder      |
   |                        |
   |------------------------|
              |
              |
     Splunk Enterprise (Host)
  SIEM - Detection - Alerting - Dashboards

---

# Technologies Used

## Infrastructure

- Windows Server 2025 (Server Core)
- Windows 11 Pro
- Oracle VirtualBox

## Active Directory

- Active Directory Domain Services (AD DS)
- DNS
- PowerShell Administration
- User Management
- Organizational Units (OUs)
- Group Policy Objects (GPO)

## Security Operations

- Splunk Enterprise (SIEM)
- Splunk Universal Forwarder
- Windows Advanced Audit Policy
- Windows Security Event Monitoring
- SPL (Search Processing Language)
- Detection Engineering & Alerting
- SOC Dashboard Development
- MITRE ATT&CK Framework
- Kali Linux (Attack Simulation)
- Hydra (Brute Force Testing)

---

# Completed Work

## ✅ Active Directory Deployment

Built and configured a Windows enterprise domain environment.

Completed:

- Installed Active Directory Domain Services
- Promoted Windows Server to Domain Controller
- Created `cyberlab.local` domain
- Configured DNS services
- Verified Domain Controller functionality

### Domain Controller Verification

![Domain Controller](images/dc01-domain-controller.png)

---

## ✅ Windows Server Configuration

Configured and verified the Windows Server environment using PowerShell.

Completed:

- Server configuration
- Network configuration
- Installed server roles verification
- Active Directory validation

### Server Information

![Server Information](images/dc01-server-info.png)

### Installed Roles

![Installed Roles](images/dc01-installed-roles.png)

---

## ✅ Active Directory User Management

Created and managed domain users and organizational structure.

Implemented:

- Domain user accounts
- Organizational Units
- User organization and management

### Domain Users

![Domain Users](images/dc01-domain-users.png)

### Organizational Units

![Organizational Units](images/dc01-organizational-units.png)

---

## ✅ Windows 11 Domain Integration

Configured a Windows 11 Pro endpoint and successfully joined it to the Active Directory domain.

Verified:

- Domain membership
- Domain authentication
- Communication with Domain Controller

### Domain Membership

![Domain Membership](images/client01-domain-membership.png)

---

## ✅ Domain Authentication Verification

Validated authentication using an Active Directory domain account.

Example:

CYBERLAB\shreya.bista

Verification command:

```cmd
whoami

Authentication Verification

Domain Authentication (images/client01-domain-user-authentication.png)

---
✅ Network Configuration

Verified endpoint connectivity and Active Directory DNS configuration.

Command used:

ipconfig /all

Client Network Configuration

Network Configuration (images/client01-network-config.png)

---
Phase 2: SOC Detection & Monitoring

With the enterprise domain foundation complete, this phase builds a real attack-and-detection pipeline: simulated adversary activity generating Windows Security events, centralized log collection, and SIEM-based detection engineering.

Pipeline: Attacker activity → Windows Security events → Splunk (SIEM) → Detection → Alerting → Dashboard

---
✅ Advanced Audit Policy Configuration

Configured centralized audit logging via Group Policy to capture the security events a SOC analyst actually investigates. Since DC01 runs Server Core (no GUI, no GPMC), this was done entirely through PowerShell, editing the GPO's audit policy directly in SYSVOL.

Enabled these audit subcategories, mapped to the event IDs they generate:

┌─────────────┬──────────────────────────────────┬───────────────────────────┐
│  Event ID   │           Description            │     Audit Subcategory     │
├─────────────┼──────────────────────────────────┼───────────────────────────┤
│ 4624 / 4625 │ Successful / Failed logon        │ Logon                     │
├─────────────┼──────────────────────────────────┼───────────────────────────┤
│ 4740        │ Account locked out               │ Account Lockout           │
├─────────────┼──────────────────────────────────┼───────────────────────────┤
│ 4688        │ New process created              │ Process Creation          │
├─────────────┼──────────────────────────────────┼───────────────────────────┤
│ 4720 / 4726 │ User account created / deleted   │ User Account Management   │
├─────────────┼──────────────────────────────────┼───────────────────────────┤
│ 4728        │ Member added to a security group │ Security Group Management │
└─────────────┴──────────────────────────────────┴───────────────────────────┘

Process:
1. Used auditpol /backup on the Domain Controller to get accurate subcategory names and GUIDs.
2. Built a minimal audit.csv targeting only the subcategories above.
3. Deployed it into the GPO's SYSVOL folder (...\Policies\{GUID}\Machine\Microsoft\Windows NT\Audit\audit.csv).
4. Registered the Security Settings client-side extension on the GPO object so Windows would actually process the file.
5. Manually incremented the GPO's version number so CLIENT01 would detect and pull the change.

Audit Policy Verification

Audit Policy Configuration (images/client01-audit-policy-config.png)

---
✅ Attack Simulation — RDP Brute Force

Used Kali Linux as a controlled attacker VM to simulate a real brute-force attack against a domain user account over RDP, generating authentic, detectable evidence.

Target: john.employee (domain user) via RDP (port 3389) on CLIENT01
Tool: Hydra, run from Kali (192.168.56.30)

hydra -l john.employee -P passwords.txt rdp://192.168.56.20 -t 1 -V

The attack was run twice, an early attempt while the Domain Controller was offline correctly failed with "no such user" (the client couldn't validate the account at all), and a second attempt with the DC online correctly returned "wrong password", confirming realistic, working authentication validation end to end.

Attack in Progress

Hydra RDP Brute Force (images/kali-hydra-rdp-bruteforce.png)

Resulting Security Events on the Target Endpoint

Failed Logon Events (images/client01-failed-logon-events.png)

---
✅ Splunk Universal Forwarder Deployment

Installed and configured a Splunk Universal Forwarder on CLIENT01 to ship Windows Security and System event logs to a Splunk Enterprise instance for centralized analysis.

Key configuration:
- Forwarder points to the Splunk indexer at 10.0.2.2:9997 (VirtualBox's fixed host-loopback address for NAT-connected VMs)
- inputs.conf configured to monitor:
[WinEventLog://Security]
disabled = 0
index = main

[WinEventLog://System]
disabled = 0
index = main
- Opened a Windows Firewall rule on the Splunk host to allow inbound connections on port 9997

Troubleshooting note: the forwarder installer configures outbound connectivity (outputs.conf) but does not configure any log sources by default, inputs.conf ships empty. This had to be created manually before any data would flow, a good reminder that "installed and running" doesn't mean "actually collecting data."

---
✅ Detection Engineering with Splunk

Wrote SPL (Search Processing Language) queries to investigate the simulated attack and answer the core questions a SOC analyst asks: who, from where, when, and how many times.

Failed login analysis:
spl
index=main host=CLIENT01 EventCode=4625
| stats count by Account_Name, Source_Network_Address
| sort -count

Attack timeline:
spl
index=main host=CLIENT01 EventCode=4625 Account_Name=john.employee
| timechart span=1m count

Result: 13 failed login attempts against john.employee, all originating from 192.168.56.30 (the Kali attacker VM), clean, unambiguous evidence of the brute-force attempt.

Search Results

Failed Login Search (images/splunk-failed-login-search.png)

Attack Timeline

Failed Login Timechart (images/splunk-failed-login-timechart.png)

---
✅ Alerting

Built a scheduled Splunk alert to automatically detect brute-force patterns, matching a 5-or-more-failures-in-2-minutes threshold.

spl
index=main host=CLIENT01 EventCode=4625
| bucket _time span=2m
| stats count by _time, Account_Name, Source_Network_Address
| where count >= 5

Alert configuration: Scheduled, runs every 5 minutes over the last 5 minutes, triggers when results > 0.

Alert Configuration

Alert Configuration (images/splunk-alert-configuration.png)

---
⏳ SOC Monitoring Dashboard (built, screenshot pending)

Built a unified 6-panel Splunk dashboard providing at-a-glance visibility across all monitored event types, not just the brute-force scenario, a general-purpose security monitoring view.

┌──────────────────────────────┬─────────────────────────────────────────────────────────────────────────┐
│            Panel             │                                 Purpose                                 │
├──────────────────────────────┼─────────────────────────────────────────────────────────────────────────┤
│ Security Events by Type      │ Volume breakdown across all 7 monitored event IDs                       │
├──────────────────────────────┼─────────────────────────────────────────────────────────────────────────┤
│ Security Activity Over Time  │ Timeline of all event types together                                    │
├──────────────────────────────┼─────────────────────────────────────────────────────────────────────────┤
│ Failed Login Attempts (4625) │ Brute-force evidence, by account and source IP                          │
├──────────────────────────────┼─────────────────────────────────────────────────────────────────────────┤
│ Successful Logins (4624)     │ Baseline comparison                                                     │
├──────────────────────────────┼─────────────────────────────────────────────────────────────────────────┤
│ Account & Group Changes      │ Detects new users, deletions, privilege escalation via group membership │
├──────────────────────────────┼─────────────────────────────────────────────────────────────────────────┤
│ Account Lockouts             │ Confirms lockout policy enforcement                                     │
└──────────────────────────────┴─────────────────────────────────────────────────────────────────────────┘

The dashboard is fully built and functional in Splunk. The screenshot for this section is the one piece of Phase 2 still pending — will be added as images/splunk-dashboard.png once captured.

Dashboard

SOC Dashboard (images/splunk-dashboard.png)

---
MITRE ATT&CK Mapping

This scenario maps to:

- T1110 — Brute Force: repeated authentication attempts against a valid domain account
- T1021.001 — Remote Services: Remote Desktop Protocol: the specific service targeted

---
Project Documentation

Detailed documentation for each phase of the lab:

Environment Setup

Virtual machine deployment and initial lab configuration.

➡️ View Environment Setup (01-Environment-Setup/setup.md)

---
Active Directory Configuration

Domain Controller deployment, DNS configuration, user management, and Organizational Units.

➡️ View Active Directory Documentation (02-Active-Directory/active-directory.md)

---
Domain Join

Windows 11 endpoint integration and Active Directory authentication verification.

➡️ View Domain Join Documentation (03-Domain-Join/domain-join.md)

---
Group Policy Configuration

Security policies and centralized endpoint management.

➡️ View Group Policy Documentation (04-Group-Policy/group-policy.md)

---
SOC Detection Engineering

Advanced audit policy, attack simulation, Splunk log collection, detection searches, alerting, and dashboarding.

➡️ View SOC Detection Documentation (05-SOC-Detection/soc-detection.md)

---
Security Skills Demonstrated

This project demonstrates hands-on experience with:

✅ Windows Server Administration
✅ Active Directory Deployment
✅ Identity and Access Management
✅ Domain Authentication
✅ PowerShell Administration
✅ DNS Configuration
✅ User and Access Management
✅ Group Policy Configuration
✅ Endpoint Management
✅ Cybersecurity Lab Development
✅ SIEM Deployment & Configuration
✅ Log Collection & Forwarding
✅ SPL Query Development
✅ Detection Rule Engineering
✅ Security Alerting
✅ SOC Dashboard Development
✅ Attack Simulation & Penetration Testing Basics
✅ MITRE ATT&CK Mapping
✅ Security Incident Investigation

---
Development Roadmap

Phase 2: SOC Monitoring Environment ✅ Functionally Complete

- [x] Enable advanced Windows auditing
- [x] Configure Windows event collection
- [x] Integrate Splunk Enterprise
- [x] Monitor authentication events
- [x] Detect brute-force attacks
- [x] Create detection rules
- [x] Build SOC monitoring dashboard
- [x] Map activity to MITRE ATT&CK techniques
- [ ] Add final dashboard screenshot to documentation
- [ ] Deploy Sysmon for deeper process/network visibility (future phase)

Phase 3: Expanded Detection Scenarios ⏳ Planned

- [ ] Simulate privilege escalation (add user to privileged group)
- [ ] Simulate suspicious PowerShell activity
- [ ] Multi-host correlation

---
Related Cybersecurity Projects

Other hands-on security projects:

- Microsoft Sentinel Failed Login Detection Lab
- Splunk Windows Authentication Monitoring & Brute Force Detection Lab
- Python Security Log Analyzer
- Wireshark Malware Traffic Analysis

---
About Me

Shreya Bista

Cybersecurity Graduate | CompTIA Security+ Certified

Interested in Security Operations, Threat Detection, and Defensive Security Engineering.
