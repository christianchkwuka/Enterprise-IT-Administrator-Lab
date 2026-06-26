# 01 Active Directory Administration

## Project Overview / ProjektÃ¼bersicht

This module documents the installation and full configuration of Active Directory Domain Services (AD DS) in a virtual enterprise IT lab environment using Windows Server 2022.

Dieses Modul dokumentiert die Installation und vollstÃ¤ndige Konfiguration von Active Directory Domain Services (AD DS) in einer virtuellen IT-Lab-Umgebung mit Windows Server 2022.

The objective was to build a structured, enterprise-style domain environment with Organizational Units, security groups, user accounts, and Group Policy Objects â demonstrating real-world IT administration and Identity & Access Management skills.

Ziel war der Aufbau einer strukturierten, unternehmensnahen DomÃ¤nenumgebung mit Organisationseinheiten, Sicherheitsgruppen, Benutzerkonten und Gruppenrichtlinien â zur Demonstration praxisnaher IT-Administration und Identity & Access Management.

---

## Lab Environment / Lab-Umgebung

* Windows Server 2022
* Active Directory Domain Services (AD DS)
* DNS Server (integrated with AD)
* Group Policy Management Console (GPMC)
* Active Directory Users and Computers (ADUC)
* Oracle VirtualBox
* Domain / DomÃ¤ne: `grclab.local`
* Server Name / Servername: `WIN-JTS1CJ3NE68`
* Domain Controller IP: `192.168.56.26`

---

## Project Goal / Projektziel

The goal of this module was to install, configure, and validate a fully functional Active Directory domain that simulates a small enterprise IT environment.

Ziel dieses Moduls war die Installation, Konfiguration und Validierung einer vollstÃ¤ndig funktionsfÃ¤higen Active-Directory-DomÃ¤ne, die eine kleine Unternehmens-IT-Umgebung simuliert.

Expected result / Erwartetes Ergebnis:

```text
Domain Controller: WIN-JTS1CJ3NE68.grclab.local
Domain: grclab.local
Organizational Units: HR, Finance, IT, Sales, Management
Security Groups: HR_Team, Finance_Team, IT_Team, Sales_Team
Users: Department users assigned to correct OUs and groups
GPOs: Linked and applied to correct OUs
```

---

## Implemented Tasks / Umgesetzte Aufgaben

* Installed Windows Server 2022 on VirtualBox
  Windows Server 2022 auf VirtualBox installiert

* Promoted server to Domain Controller
  Server zum Domain Controller hochgestuft

* Configured DNS integration with Active Directory
  DNS-Integration mit Active Directory konfiguriert

* Created the domain `grclab.local`
  DomÃ¤ne `grclab.local` erstellt

* Designed and created Organizational Units (OUs) for each department
  Organisationseinheiten (OUs) fÃ¼r jede Abteilung entworfen und erstellt

* Created Active Directory security groups
  Active-Directory-Sicherheitsgruppen erstellt

* Created domain user accounts and assigned to correct OUs and groups
  DomÃ¤nenbenutzer erstellt und korrekt OUs und Gruppen zugewiesen

* Applied Role-Based Access Control (RBAC) and Least Privilege principle
  Rollenbasierte Zugriffskontrolle (RBAC) und Least-Privilege-Prinzip angewendet

* Configured and validated Group Policy Objects (GPOs)
  Gruppenrichtlinien (GPOs) konfiguriert und validiert

* Validated domain join for Windows 11 client
  Domain-Beitritt des Windows-11-Clients validiert

---

## Domain Configuration / DomÃ¤nenkonfiguration

The domain `grclab.local` was configured as follows:

Die DomÃ¤ne `grclab.local` wurde wie folgt konfiguriert:

```text
Domain Name:         grclab.local
NetBIOS Name:        GRCLAB
Forest Level:        Windows Server 2016
Domain Level:        Windows Server 2016
Domain Controller:   WIN-JTS1CJ3NE68
DC IP Address:       192.168.56.26
DNS Server:          192.168.56.26 (integrated)
```

---

## Organizational Unit Structure / Organisationseinheiten-Struktur

The following OU structure was created to reflect a realistic enterprise department hierarchy:

Folgende OU-Struktur wurde erstellt, um eine realistische Abteilungshierarchie eines Unternehmens abzubilden:

```text
grclab.local
âââ Company (root OU)
    âââ HR
    â   âââ Users
    âââ Finance
    â   âââ Users
    âââ IT
    â   âââ Users
    âââ Sales
    â   âââ Users
    âââ Management
        âââ Users
```

Each department OU contains its own Users sub-OU for organised user management.

Jede Abteilungs-OU enthÃ¤lt eine eigene Benutzer-Unter-OU fÃ¼r geordnete Benutzerverwaltung.

---

## Security Groups / Sicherheitsgruppen

Department-based security groups were created for access control:

Abteilungsbasierte Sicherheitsgruppen wurden fÃ¼r die Zugriffskontrolle erstellt:

| Group Name | Type | Scope | Purpose |
|------------|------|-------|---------|
| HR_Team | Security | Global | HR department access |
| Finance_Team | Security | Global | Finance department access |
| IT_Team | Security | Global | IT administration access |
| Sales_Team | Security | Global | Sales department access |
| IT_Admins | Security | Global | Elevated IT administrative rights |

Access to file shares, GPOs, and resources was assigned via these groups â not directly to individual users.

Der Zugriff auf Dateifreigaben, GPOs und Ressourcen wurde Ã¼ber diese Gruppen vergeben â nicht direkt an einzelne Benutzer.

---

## User Accounts / Benutzerkonten

Example users were created for each department:

Beispielbenutzer wurden fÃ¼r jede Abteilung erstellt:

| Username | Department | OU | Group |
|----------|------------|-----|-------|
| Friedrich.helmut | HR | HR/Users | HR_Team |
| Maria.schulz | Finance | Finance/Users | Finance_Team |
| admin.christian | IT | IT/Users | IT_Team, IT_Admins |
| Jonas.weber | Sales | Sales/Users | Sales_Team |

All users were configured with:

Alle Benutzer wurden konfiguriert mit:

```text
Password must be changed at next login: Yes
Account enabled: Yes
User Principal Name: firstname.lastname@grclab.local
```

---

## Group Policy Objects / Gruppenrichtlinien

The following GPOs were configured and linked:

Folgende GPOs wurden konfiguriert und verknÃ¼pft:

| GPO Name | Linked To | Purpose |
|----------|-----------|---------|
| Password_Policy | grclab.local | Enforce strong password requirements |
| Map_HR_Drive | HR OU | Automatically map H: drive for HR users |
| Desktop_Restrictions | Company OU | Apply desktop policy baseline |
| Disable_USB_Storage | Company OU | Block USB storage devices |

---

## Password Policy Configuration / Passwort-Richtlinie

A strong password policy was configured at domain level:

Eine starke Passwortrichtlinie wurde auf DomÃ¤nenebene konfiguriert:

```text
Minimum password length:    12 characters
Password complexity:        Enabled
Maximum password age:       90 days
Minimum password age:       1 day
Password history:           24 passwords remembered
Account lockout threshold:  5 failed attempts
Lockout duration:           30 minutes
```

---

## Validation / Validierung

### Domain Controller Validation / Domain-Controller-Validierung

```cmd
dcdiag /v
```

Expected result / Erwartetes Ergebnis:

```text
Directory Server Diagnosis
...
passed test Connectivity
passed test Advertising
passed test FrsEvent
passed test DFSREvent
passed test SysVolCheck
passed test NetLogons
passed test Services
passed test Replications
passed test RidManager
passed test MachineAccount
```

---

### DNS Validation / DNS-Validierung

```cmd
nslookup grclab.local
```

Expected result / Erwartetes Ergebnis:

```text
Server:  WIN-JTS1CJ3NE68.grclab.local
Address: 192.168.56.26

Name:    grclab.local
Address: 192.168.56.26
```

---

### Domain Join Validation (Windows 11 Client) / Domain-Beitritt-Validierung

```cmd
whoami /fqdn
```

Expected result / Erwartetes Ergebnis:

```text
grclab\Friedrich.helmut
```

---

### Group Membership Validation / Gruppmitgliedschaft prÃ¼fen

```cmd
net user Friedrich.helmut /domain
```

Expected result / Erwartetes Ergebnis:

```text
Global Group memberships: HR_Team
```

---

## Troubleshooting / Fehlerbehebung

### DNS not resolving after DC promotion / DNS lÃ¶st nach DC-Hochstufung nicht auf

Possible cause / MÃ¶gliche Ursache:

* Client DNS server not pointing to Domain Controller
  Client-DNS-Server zeigt nicht auf den Domain Controller

Resolution / LÃ¶sung:

```text
Set client DNS to 192.168.56.26 (Domain Controller IP)
```

---

### User cannot log into domain / Benutzer kann sich nicht an DomÃ¤ne anmelden

Possible causes / MÃ¶gliche Ursachen:

* Account disabled or locked out
  Konto deaktiviert oder gesperrt

* Incorrect OU placement
  Falsche OU-Zuordnung

* Replication issue (if multiple DCs)
  Replikationsproblem (bei mehreren DCs)

Resolution / LÃ¶sung:

```text
Check ADUC â User â Account tab â Unlock / Enable account
Run: gpupdate /force on client
```

---

## Evidence / Screenshots / Nachweise

| Screenshot | Description / Beschreibung |
|------------|---------------------------|
| `01_ad_ds_installation.png` | AD DS role installation / Installation der AD-DS-Rolle |
| `02_domain_promotion.png` | Server promotion to Domain Controller / Hochstufung zum Domain Controller |
| `03_ou_structure.png` | Organizational Unit structure in ADUC / OU-Struktur in ADUC |
| `04_security_groups.png` | Security groups created / Erstellte Sicherheitsgruppen |
| `05_user_accounts.png` | Domain user accounts / DomÃ¤nen-Benutzerkonten |
| `06_user_group_membership.png` | User group membership / Gruppenmitgliedschaft der Benutzer |
| `07_gpo_overview.png` | GPO overview in Group Policy Management / GPO-Ãbersicht in der Gruppenrichtlinienverwaltung |
| `08_password_policy.png` | Password policy configuration / Passwortrichtlinien-Konfiguration |
| `09_dcdiag_output.png` | dcdiag validation output / dcdiag-Validierungsausgabe |
| `10_domain_join_client.png` | Windows 11 client joined to domain / Windows-11-Client in DomÃ¤ne eingebunden |

Screenshots are stored in:

```text
evidence/01_Active_Directory/
```

---

## Skills Demonstrated / Nachgewiesene Kompetenzen

* Windows Server 2022 Installation & Configuration / Installation und Konfiguration
* Active Directory Domain Services (AD DS) setup
* Domain Controller promotion / Domain-Controller-Hochstufung
* DNS integration with Active Directory / DNS-Integration mit Active Directory
* Organizational Unit (OU) design and creation / OU-Design und -Erstellung
* Security group creation and management / Erstellung und Verwaltung von Sicherheitsgruppen
* Domain user lifecycle management / Benutzerlebenszyklus-Management
* Role-Based Access Control (RBAC) / Rollenbasierte Zugriffskontrolle
* Least Privilege implementation / Least-Privilege-Umsetzung
* Group Policy Object (GPO) configuration / GPO-Konfiguration
* Password policy enforcement / Passwortrichtlinien-Durchsetzung
* Domain join and client administration / Domain-Beitritt und Client-Administration
* AD troubleshooting using dcdiag, nslookup / Fehlerbehebung mit dcdiag, nslookup
* Identity & Access Management (IAM) fundamentals

---

## Business Relevance / Praxisrelevanz

Active Directory is the backbone of identity and access management in virtually every enterprise Windows environment. Administrators who can install, configure, and maintain AD are essential in any IT team.

Active Directory ist das RÃ¼ckgrat der IdentitÃ¤ts- und Zugriffsverwaltung in nahezu jeder Unternehmens-Windows-Umgebung. Administratoren, die AD installieren, konfigurieren und warten kÃ¶nnen, sind in jedem IT-Team unverzichtbar.

This module demonstrates the ability to:

Dieses Modul demonstriert die FÃ¤higkeit:

* build a structured domain from scratch
  eine strukturierte DomÃ¤ne von Grund auf aufzubauen

* implement enterprise-grade access controls
  unternehmensweite Zugriffskontrollen umzusetzen

* manage the identity lifecycle of users and groups
  den IdentitÃ¤tslebenszyklus von Benutzern und Gruppen zu verwalten

* configure security baseline policies
  Sicherheits-Grundlinienrichtlinien zu konfigurieren

* document and validate all configurations professionally
  alle Konfigurationen professionell zu dokumentieren und zu validieren

---

## Result / Ergebnis

A fully functional Active Directory domain `grclab.local` was successfully built and configured. The domain controller was promoted, DNS integrated, Organizational Units and security groups created, domain users assigned to appropriate groups, and Group Policy Objects configured and validated.

Eine vollstÃ¤ndig funktionsfÃ¤hige Active-Directory-DomÃ¤ne `grclab.local` wurde erfolgreich aufgebaut und konfiguriert. Der Domain Controller wurde hochgestuft, DNS integriert, Organisationseinheiten und Sicherheitsgruppen erstellt, DomÃ¤nenbenutzer den entsprechenden Gruppen zugewiesen und Gruppenrichtlinien konfiguriert und validiert.

This module demonstrates practical enterprise-level Active Directory administration skills essential for any IT Administrator or System Administrator role.

Dieses Modul zeigt praxisnahe Active-Directory-Administrationskenntnisse auf Unternehmensebene, die fÃ¼r jede IT-Administrator- oder Systemadministrator-Rolle unverzichtbar sind.
