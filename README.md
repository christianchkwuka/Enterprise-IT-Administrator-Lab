
# Enterprise IT Administrator Lab

**Windows Server 2022 | Active Directory | M365 & Entra ID | Intune | Endpoint-Protection | pfSense | WLAN & Netzwerksegmentierung | Monitoring | Backup | ISMS | Change Management | GRC Documentation**

---

## Projektübersicht / Project Overview

This project demonstrates a practical enterprise-style IT administration lab environment built with virtualization technologies. The lab simulates common tasks performed by an IT Administrator, System Administrator, IT Support Specialist, and GRC-oriented Infrastructure Administrator.

Dieses Projekt zeigt eine praxisnahe Enterprise-IT-Administrator-Lab-Umgebung, die mit Virtualisierungstechnologien aufgebaut wurde. Das Lab simuliert typische Aufgaben eines IT-Administrators, Systemadministrators, IT-Support-Spezialisten sowie eines GRC-orientierten Infrastruktur-Administrators.

**Core focus areas / Schwerpunkte:**
- Windows Server Administration & Serverlandschaft
- Active Directory, Group Policy Objects, Benutzer- und Gruppenverwaltung
- Client Management & Endpoint-Protection
- Microsoft 365, Entra ID, Intune (MDM) und Exchange Online
- Netzwerk- und WLAN-Segmentierung mit pfSense (VLANs, Firewall-Regeln)
- Monitoring (Checkmk / Wazuh), Backup & Restore (Veeam)
- Informationssicherheit (ISMS) & GRC-Dokumentation
- Change Management & technische Prozessdokumentation

---

## Ziel des Projekts / Project Objective

The objective of this lab is to demonstrate hands-on IT administration skills in a structured and documented environment — covering the full lifecycle from installation and configuration to monitoring, security validation, and audit documentation.

Ziel dieses Labs ist es, praktische IT-Administrationskenntnisse in einer strukturierten und dokumentierten Umgebung nachzuweisen — vom Aufbau und der Konfiguration bis hin zu Monitoring, IT-Security und Audit-Dokumentation.

**Demonstrated capabilities:**
- Install and configure Windows Server environments (Windows Server 2022, Windows 11)
- Manage Active Directory users, groups, organisational units and Group Policy Objects
- Administer Microsoft 365, Entra ID, Intune and Exchange Online
- Implement Endpoint-Protection and Client Management
- Configure network segmentation and WLAN with pfSense (VLANs, DHCP, Firewall)
- Validate firewall rules and control access (Kontrolle der Zugriffe)
- Set up monitoring and log analysis (Checkmk, Wazuh / SIEM basics)
- Configure backup and restore processes (Veeam)
- Document IT processes, change requests and audit evidence professionally
- Apply ISMS principles, BSI IT-Grundschutz and GRC concepts

---

## Lab Architecture / Lab-Architektur

The lab is built using Oracle VirtualBox and consists of multiple virtual machines representing a small enterprise IT environment.

Das Lab wurde mit Oracle VirtualBox aufgebaut und besteht aus mehreren virtuellen Maschinen, die eine kleine Unternehmens-IT-Umgebung simulieren.

### Main Components

| Component | Purpose |
|-----------|---------|
| Windows Server 2022 | Active Directory, DNS, File Server, Group Policy, Serverlandschaft |
| Windows Client (Windows 11) | Domain client — Client Management, Endpoint-Protection testing |
| pfSense Firewall | Routing, firewall rules, WLAN segmentation, DHCP, VLANs |
| Kali Linux | Security testing, firewall validation |
| Ubuntu Server | Monitoring / SIEM / infrastructure services |
| Checkmk / Wazuh | Monitoring, log analysis, ISMS evidence |
| Veeam Backup Server | Backup, restore testing, disaster recovery |
| VirtualBox | Virtualization platform |

### Network Architecture / Netzwerkarchitektur

| Network Zone | Purpose | Example |
|-------------|---------|---------|
| LAN / Management | Server and management network | 192.168.56.0/24 |
| HR / Personalwesen | HR client network (WLAN simulation) | 10.0.3.0/24 |
| DMZ | Isolated network for exposed systems | VLAN / internal |
| Finance | Sensitive finance network | VLAN / internal |
| IT | Administrative network | VLAN / internal |
| ATTACK_NET | Security testing network | Kali / Metasploitable |

### Example IP Addresses

| System | IP Address |
|--------|-----------|
| pfSense Web GUI | 192.168.56.100 |
| Windows Server / Domain Controller | 192.168.56.26 |
| HR Gateway on pfSense | 10.0.3.2 |
| Kali HR Client | 10.0.3.x |
| Monitoring / Wazuh Server | 192.168.56.102 |

---

## Repository Structure / Projektstruktur

```
Enterprise-IT-Administrator-Lab/
│
├── README.md
├── diagrams/
│   └── Netzwerkarchitektur.png
│
├── docs/
│   ├── 01_Active_Directory/
│   ├── 02_File_Server_Access_Control/
│   ├── 03_GPO_Drive_Mapping/
│   ├── 04_Backup_and_Restore/
│   ├── 05_pfSense_Network_Segmentation/
│   ├── 06_VPN_Remote_Access/
│   ├── 07_Monitoring_and_Logs/
│   ├── 08_Microsoft_365_Entra_IAM/
│   ├── 09_Ticketing_Process/
│   └── 10_Audit_Documentation/
│
├── evidence/
│   ├── 01_Active_Directory/
│   ├── 02_File_Server_Access_Control/
│   ├── 03_GPO_Drive_Mapping/
│   ├── 04_Backup_and_Restore/
│   ├── 05_pfSense_Network_Segmentation/
│   ├── 06_VPN_Remote_Access/
│   ├── 07_Monitoring_and_Logs/
│   ├── 08_Microsoft_365_Entra_IAM/
│   ├── 09_Ticketing_Process/
│   └── 10_Audit_Documentation/
│
├── scripts/
│   ├── powershell/
│   └── bash/
│
└── templates/
    ├── audit_checklists/
    ├── risk_assessment/
    └── documentation_templates/
```

---

## Modules / Projektmodule

### 01 Active Directory Administration

This module demonstrates the installation and administration of Active Directory Domain Services including user lifecycle management, Group Policy and role-based access control.

**Implemented Tasks:**
- Installed Windows Server 2022
- Configured Active Directory Domain Services (AD DS)
- Created domain structure and Organizational Units (OUs)
- Created users, security groups and managed memberships
- Applied role-based access control (RBAC) and least privilege
- Configured and validated Group Policy Objects (GPOs)

**Skills Demonstrated:** Windows Server Administration · Active Directory · User & Group Management · OU Design · GPO · RBAC · Identity & Access Management (IAM)

---

### 02 File Server Access Control

This module demonstrates the configuration of a Windows File Server with NTFS permissions, SMB shares and group-based access control.

**Implemented Tasks:**
- Created shared folders for departments (HR, Finance, IT, Sales)
- Configured SMB shares and NTFS permissions
- Applied group-based access control (least privilege)
- Tested authorised and unauthorised access
- Documented access control results as audit evidence

**Skills Demonstrated:** File Server Administration · NTFS Permission Management · SMB Share Configuration · Least Privilege · Access Control Validation · Security Documentation

---

### 03 GPO Drive Mapping

This module demonstrates the use of Group Policy Objects to automatically map network drives for domain users.

**Implemented Tasks:**
- Created GPO for HR drive mapping
- Linked GPO to the correct Organisational Unit
- Configured Drive Maps under Group Policy Preferences
- Tested GPO application on client system (Windows 11)
- Validated results using `gpupdate /force` and `gpresult /r`

**Example Configuration:**
- Network Share: `\\WIN-JTS1CJ3NE68\HR` | Drive Letter: `H:` | Target: HR users

**Skills Demonstrated:** Group Policy Management · Drive Mapping · Windows Client Administration · Client Management · GPO Troubleshooting · Enterprise User Environment

---

### 04 Backup and Restore

This module demonstrates backup and restore procedures using Windows Server Backup and Veeam Backup & Replication.

**Implemented Tasks:**
- Created backup repository and configured backup storage
- Installed and configured Veeam Backup & Replication
- Created and scheduled backup jobs
- Tested file-level restore and validated successful recovery
- Documented backup and restore processes as operational evidence

**Backup Test Scenario:**
1. Create test file → Run backup job → Delete test file → Restore from backup → Validate recovery

**Skills Demonstrated:** Backup Planning · Restore Validation · Veeam Administration · Disaster Recovery · Operational Resilience · IT Documentation

---

### 05 pfSense Network Segmentation & WLAN

This module demonstrates network segmentation using pfSense firewall rules, VLANs, DHCP and access control across multiple network zones — including WLAN-simulated environments.

**Implemented Tasks:**
- Configured pfSense interfaces and VLANs
- Created segmented networks (HR, Finance, IT, DMZ)
- Configured DHCP for network zones
- Designed and implemented firewall rules (block / allow)
- Validated rules using ping tests and firewall log review
- Documented Kontrolle der Zugriffe (access control)

**Firewall Rule Example:**
```
Action: Block | Interface: HR | Protocol: IPv4 Any
Source: HR net | Destination: Domain Controller (192.168.56.26)
Result: 100% packet loss — HR successfully blocked from DC
```

**Skills Demonstrated:** pfSense Administration · Firewall Rule Design · Network Segmentation · WLAN Segmentation · VLANs · Routing & DHCP · Packet Filtering · Security Validation · Kontrolle der Zugriffe

---

### 06 VPN Remote Access

This module demonstrates secure remote access using VPN technologies on pfSense.

**Planned / In Progress:**
- Configure VPN service on pfSense (OpenVPN)
- Create VPN user access and certificates
- Test and validate remote connection
- Document VPN configuration and access restrictions

**Skills Demonstrated:** Remote Access Security · VPN Configuration · pfSense VPN · Secure Administration Access

---

### 07 Monitoring, Logs & ISMS

This module demonstrates infrastructure monitoring, log collection and basic ISMS evidence generation using Checkmk and Wazuh.

**Implemented Tasks:**
- Installed Checkmk monitoring server and created site
- Added Linux and Windows Server hosts with agents
- Configured firewall access for monitoring (port 6556)
- Discovered services and activated monitoring changes
- Installed and configured Wazuh for log analysis and SIEM basics
- Collected monitoring evidence for ISMS documentation

**Example Systems:**
- Monitoring Server: 192.168.56.24 | Windows Server: 192.168.56.26

**Skills Demonstrated:** Infrastructure Monitoring · Windows & Linux Agent Installation · Service Discovery · Log Analysis · ISMS Evidence Collection · Wazuh / SIEM Basics · Troubleshooting · IT-Security

---

### 08 Microsoft 365 / Entra ID / Intune & Endpoint-Protection

This module documents identity and access management using Microsoft 365, Microsoft Entra ID and Intune, including Endpoint-Protection and Mobile Device Management (MDM).

**Implemented / Documented Tasks:**
- User and group management in Entra ID and M365
- MFA configuration and Conditional Access review
- Admin role review and privilege management
- Intune device enrolment and Endpoint-Protection policies (MDM)
- Mobile Device Management (MDM) configuration basics
- Access review documentation and IAM evidence
- Exchange Online and Teams administration

**Skills Demonstrated:** Microsoft 365 Administration · Entra ID · Intune (MDM) · Endpoint-Protection · MFA · Conditional Access · Exchange Online · IAM Documentation · Least Privilege · Cloud Identity Management

---

### 09 Ticketing & Change Management

This module documents a practical IT support ticketing process and change management workflow based on ITIL-oriented procedures.

**Example Change Management Workflow:**
1. Change Request received and documented
2. Risk assessment and impact analysis
3. Approval and scheduling
4. Implementation and validation
5. Documentation and closure

**Example Ticket Categories:**
Password reset · Account locked · Network issue · Printer issue · Software installation · Access request · Backup failure · Monitoring alert · Change Request

**Skills Demonstrated:** IT Support Process · Incident Management · Change Management · Service Request Handling · SLA Awareness · Technical Communication · ITIL Basics · Documentation

---

### 10 Audit Documentation & ISMS

This module connects technical implementation with audit and compliance documentation, mapping controls to relevant IT security standards.

**Implemented / Planned Tasks:**
- Create audit evidence and screenshot documentation
- Document implemented controls and security measures
- Map technical controls to security standards (ISO 27001, BSI IT-Grundschutz, NIST CSF)
- Identify risks and create remediation notes
- Prepare ISMS-ready audit documentation

**Example Standards:**

| Standard | Relevance |
|----------|-----------|
| ISO/IEC 27001 | Information security controls |
| NIST CSF | Cybersecurity framework |
| BSI IT-Grundschutz | German IT security baseline |
| GDPR / DSGVO | Data protection requirements |
| ITIL | IT service management |

**Skills Demonstrated:** IT Audit Documentation · ISMS · Control Mapping · Evidence Collection · Risk Assessment · Compliance Awareness · GRC · BSI IT-Grundschutz Basics

---

## Tools and Technologies

| Category | Tools / Technologies |
|----------|---------------------|
| Virtualization | Oracle VirtualBox |
| Server OS | Windows Server 2022 |
| Client OS | Windows 11, Kali Linux |
| Directory Services | Active Directory Domain Services, Entra ID |
| Policy & Client Mgmt | Group Policy (GPO), Intune (MDM), Endpoint-Protection |
| Firewall / Network | pfSense, VLANs, WLAN Segmentation, Routing, Switching |
| Monitoring / SIEM | Checkmk, Wazuh |
| Backup | Veeam Backup & Replication, Windows Server Backup |
| Cloud | Microsoft 365, Entra ID, Intune, Exchange Online |
| Scripting | PowerShell, Bash |
| Security / ISMS | IT-Security, ISMS, Change Management, GRC |
| Documentation | Markdown, GitHub |
| Security Testing | Kali Linux, ping, traceroute, firewall logs |

---

## Key IT Security & Administration Concepts

| Concept | Implementation |
|---------|---------------|
| Least Privilege | NTFS permissions, AD RBAC, Entra ID roles |
| Network Segmentation | pfSense VLANs, WLAN zones, firewall rules |
| Endpoint-Protection | Intune MDM, Endpoint policies, Client Management |
| Kontrolle der Zugriffe | Firewall rule validation, NTFS audit, AD access reviews |
| ISMS | Wazuh log evidence, monitoring alerts, audit documentation |
| Change Management | Documented change requests, validation, closure |
| Backup & Recovery | Veeam restore tests, disaster recovery evidence |
| Identity & Access Management | Active Directory, Entra ID, MFA, Conditional Access |

---

## Current Status

| Module | Status |
|--------|--------|
| 01 Active Directory | Completed |
| 02 File Server Access Control | Completed |
| 03 GPO Drive Mapping | Completed |
| 04 Backup and Restore | In Progress |
| 05 pfSense Network Segmentation & WLAN | Completed |
| 06 VPN Remote Access | Planned |
| 07 Monitoring, Logs & ISMS | In Progress |
| 08 Microsoft 365 / Entra ID / Intune / Endpoint-Protection | In Progress |
| 09 Ticketing & Change Management | In Progress |
| 10 Audit Documentation & ISMS | In Progress |

---

## Interview Explanation (DE/EN)

**Deutsch:**
In meinem Enterprise IT Administrator Lab habe ich eine virtuelle Unternehmensumgebung mit Windows Server 2022, Active Directory, pfSense, Monitoring und Backup aufgebaut. Ich habe Benutzer, Gruppen und Organisationseinheiten verwaltet, Gruppenrichtlinien konfiguriert, Dateiserver-Zugriffe über NTFS und SMB abgesichert sowie Netzlaufwerke per GPO zugeordnet.

Mit pfSense habe ich eine Netzwerksegmentierung inkl. WLAN-Zonen und VLANs umgesetzt und Firewall-Regeln validiert. Im Bereich Microsoft 365 habe ich Entra ID, Intune (MDM), Endpoint-Protection und Exchange Online administriert. Monitoring erfolgte mit Checkmk und Wazuh als SIEM-Grundlage. Backup- und Restore-Prozesse wurden mit Veeam dokumentiert und validiert.

Das Projekt zeigt meine praktischen Kenntnisse in Windows Server Administration, Client Management, Endpoint-Protection, Netzwerkgrundlagen, IT-Security, ISMS, Change Management sowie technischer und auditgerechter Dokumentation.

**English:**
In my Enterprise IT Administrator Lab, I built a virtual enterprise environment using Windows Server 2022, Active Directory, pfSense, monitoring and backup technologies. I managed users, groups and OUs in Active Directory, configured Group Policy Objects, secured file server access using NTFS permissions, and mapped network drives via GPO.

I implemented network segmentation with pfSense including WLAN zones and VLANs, and validated firewall rules. In the Microsoft 365 space, I administered Entra ID, Intune (MDM), Endpoint-Protection and Exchange Online. Monitoring was implemented with Checkmk and Wazuh. Backup and restore processes were validated using Veeam.

The project demonstrates practical skills in Windows Server administration, Client Management, Endpoint-Protection, networking, IT-Security, ISMS, Change Management and professional audit-ready documentation.

---

## Skills Demonstrated for IT Administrator Roles

### Technical Skills
- Windows Server 2022 Administration (Serverlandschaft)
- Active Directory, Entra ID, Group Policy (GPO)
- Client Management & Endpoint-Protection (Intune / MDM)
- Microsoft 365, Exchange Online, Teams, SharePoint
- pfSense Firewall Administration
- Network Segmentation, VLANs, WLAN, Routing & Switching
- DHCP, DNS, TCP/IP
- Kontrolle der Zugriffe (Access Control Validation)
- Monitoring (Checkmk), Log Analysis (Wazuh / SIEM)
- Backup & Restore (Veeam), Disaster Recovery
- ISMS & IT-Security fundamentals
- Change Management documentation
- PowerShell & Bash scripting basics
- Technical documentation (Markdown, GitHub)

### Professional Skills
- Structured problem solving & troubleshooting
- Documentation discipline & audit readiness
- Security awareness & ISMS thinking
- Change Management & process-oriented approach
- Communication of technical concepts (DE/EN)
- Continuous learning & adaptability

---

*This repository is actively maintained and extended. Contributions, feedback and questions are welcome.*

**GitHub:** [christianchkwuka/Enterprise-IT-Administrator-Lab](https://github.com/christianchkwuka/Enterprise-IT-Administrator-Lab)
