
# 02 File Server Access Control / Dateiserver-Zugriffskontrolle

## Project Overview / Projektübersicht

This module documents the configuration of a Windows File Server with department-based access control using Active Directory security groups, SMB shares, and NTFS permissions.

Dieses Modul dokumentiert die Einrichtung eines Windows-Dateiservers mit abteilungsbasierter Zugriffskontrolle über Active-Directory-Sicherheitsgruppen, SMB-Freigaben und NTFS-Berechtigungen.

The objective was to provide shared folders for departments such as HR, Finance, IT, and Sales while ensuring that users only have access to the folders they are authorized to use.

Ziel war es, gemeinsame Ordner für Abteilungen wie HR, Finance, IT und Sales bereitzustellen und sicherzustellen, dass Benutzer nur Zugriff auf die Ordner erhalten, für die sie berechtigt sind.

---

## Lab Environment / Lab-Umgebung

* Windows Server 2022
* Active Directory Domain Services
* File and Storage Services
* SMB Shares / SMB-Freigaben
* NTFS Permissions / NTFS-Berechtigungen
* Domain / Domäne: `grclab.local`
* Server Name / Servername: `WIN-JTS1CJ3NE68`
* Shared Folder Root / Stammordner: `C:\CompanyShares`

---

## Project Goal / Projektziel

The goal of this module was to implement secure and structured access to department folders through Active Directory groups.

Ziel dieses Moduls war es, einen sicheren und strukturierten Zugriff auf Abteilungsordner über Active-Directory-Gruppen umzusetzen.

Expected result / Erwartetes Ergebnis:

```text
HR users       → Access only to HR folder
Finance users  → Access only to Finance folder
IT admins      → Administrative access
Unauthorized users → Access denied
```

---

## Implemented Tasks / Umgesetzte Aufgaben

* Created a central folder structure under `C:\CompanyShares`
  Zentrale Ordnerstruktur unter `C:\CompanyShares` erstellt

* Created department folders for HR, Finance, IT, and Sales
  Abteilungsordner für HR, Finance, IT und Sales erstellt

* Created Active Directory security groups
  Active-Directory-Sicherheitsgruppen erstellt

* Added users to the correct department groups
  Benutzer den passenden Abteilungsgruppen hinzugefügt

* Configured SMB sharing
  SMB-Freigaben konfiguriert

* Configured NTFS permissions
  NTFS-Berechtigungen eingerichtet

* Tested successful access for authorized users
  Erfolgreichen Zugriff für berechtigte Benutzer getestet

* Tested access denial for unauthorized users
  Zugriff für nicht berechtigte Benutzer getestet und verweigert

---

## Folder Structure / Ordnerstruktur

```text
C:\CompanyShares
├── HR
├── Finance
├── IT
└── Sales
```

---

## Security Groups / Sicherheitsgruppen

Example security groups used in this lab:

Beispielhafte Sicherheitsgruppen in diesem Lab:

```text
HR_Team
Finance_Team
IT_Team
Sales_Team
```

Access was assigned through groups, not directly to individual users.

Der Zugriff wurde über Gruppen vergeben, nicht direkt an einzelne Benutzer.

This follows the principle of Role-Based Access Control and makes permission management easier, cleaner, and more scalable.

Dies folgt dem Prinzip der rollenbasierten Zugriffskontrolle und macht die Berechtigungsverwaltung einfacher, sauberer und skalierbarer.

---

## Example Access Control / Beispiel Zugriffskontrolle

```text
Finance user → Finance_Team → Access to Finance folder
HR user      → HR_Team      → Access to HR folder
Sales user   → Sales_Team   → Access to Sales folder
```

Unauthorized users should receive an access denied message.

Nicht berechtigte Benutzer sollen eine Zugriff-verweigert-Meldung erhalten.

---

## SMB Share Configuration / SMB-Freigabe-Konfiguration

The department folders were shared using SMB.

Die Abteilungsordner wurden über SMB freigegeben.

Example / Beispiel:

```text
\\WIN-JTS1CJ3NE68\HR
\\WIN-JTS1CJ3NE68\Finance
\\WIN-JTS1CJ3NE68\IT
\\WIN-JTS1CJ3NE68\Sales
```

SMB shares allow users to access folders over the network.

SMB-Freigaben ermöglichen Benutzern den Zugriff auf Ordner über das Netzwerk.

---

## NTFS Permissions / NTFS-Berechtigungen

NTFS permissions were configured on folder level.

NTFS-Berechtigungen wurden auf Ordnerebene konfiguriert.

Example for Finance folder / Beispiel für Finance-Ordner:

```text
Finance_Team:
- Modify
- Read & Execute
- List Folder Contents
- Read
- Write
```

Normal users were not granted Full Control.

Normale Benutzer erhielten keine Vollzugriffsrechte.

This prevents users from changing permissions or taking ownership of folders.

Dadurch wird verhindert, dass Benutzer Berechtigungen ändern oder Besitzrechte übernehmen.

---

## Share Permissions vs NTFS Permissions / Share-Berechtigungen vs. NTFS-Berechtigungen

Share permissions control access over the network.

Share-Berechtigungen steuern den Zugriff über das Netzwerk.

NTFS permissions control access on file and folder level.

NTFS-Berechtigungen steuern den Zugriff auf Datei- und Ordnerebene.

When both permission types apply, the most restrictive permission wins.

Wenn beide Berechtigungstypen gelten, ist die restriktivere Berechtigung wirksam.

---

## Least Privilege Principle / Least-Privilege-Prinzip

This module follows the Least Privilege principle.

Dieses Modul folgt dem Least-Privilege-Prinzip.

Users only receive the access required for their role or department.

Benutzer erhalten nur die Zugriffsrechte, die sie für ihre Rolle oder Abteilung benötigen.

Benefits / Vorteile:

* Reduced risk of unauthorized access
  Reduziertes Risiko unberechtigter Zugriffe

* Easier access management
  Einfachere Zugriffsverwaltung

* Better auditability
  Bessere Nachvollziehbarkeit

* Improved data protection
  Verbesserter Datenschutz

---

## Validation / Validierung

The access control configuration was validated through practical tests.

Die Zugriffskontrolle wurde durch praktische Tests validiert.

### Successful Access Test / Erfolgreicher Zugriffstest

An authorized user was able to access the correct department folder.

Ein berechtigter Benutzer konnte auf den richtigen Abteilungsordner zugreifen.

Example / Beispiel:

```text
Finance user → \\WIN-JTS1CJ3NE68\Finance → Access successful
```

---

### Access Denied Test / Zugriff-verweigert-Test

An unauthorized user attempted to access a folder outside their department.

Ein nicht berechtigter Benutzer versuchte, auf einen Ordner außerhalb seiner Abteilung zuzugreifen.

Example / Beispiel:

```text
HR user → \\WIN-JTS1CJ3NE68\Finance → Access denied
```

This confirms that the access control configuration works as expected.

Dies bestätigt, dass die Zugriffskontrolle wie erwartet funktioniert.

---

## Troubleshooting / Fehlerbehebung

Typical issues checked during this module:

Typische Fehler, die in diesem Modul geprüft wurden:

### User cannot access folder / Benutzer kann nicht auf Ordner zugreifen

Possible causes / Mögliche Ursachen:

* User is not in the correct AD security group
  Benutzer ist nicht in der richtigen AD-Sicherheitsgruppe

* NTFS permissions are missing or incorrect
  NTFS-Berechtigungen fehlen oder sind falsch

* SMB share permissions are too restrictive
  SMB-Freigabeberechtigungen sind zu restriktiv

* User has not logged off and back on after group change
  Benutzer hat sich nach Gruppenänderung nicht ab- und wieder angemeldet

### Network path not found / Netzwerkpfad nicht gefunden

Possible causes / Mögliche Ursachen:

* Wrong server name
  Falscher Servername

* Wrong share name
  Falscher Freigabename

* DNS issue
  DNS-Problem

* File sharing not enabled
  Dateifreigabe nicht aktiviert

---

## Evidence / Screenshots / Nachweise

The following screenshots document the implementation and validation process.

Die folgenden Screenshots dokumentieren die Umsetzung und Validierung.

| Screenshot                              | Description / Beschreibung                                                                      |
| --------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `01_companyshares_folder_structure.png` | CompanyShares folder structure / CompanyShares-Ordnerstruktur                                   |
| `02_finance_folder_properties.png`      | Finance folder properties / Eigenschaften des Finance-Ordners                                   |
| `03_smb_share_permissions.png`          | SMB share permissions / SMB-Freigabeberechtigungen                                              |
| `04_ntfs_security_permissions.png`      | NTFS security permissions / NTFS-Sicherheitsberechtigungen                                      |
| `05_ad_security_group_Finance_team.png` | Finance security group in Active Directory / Finance-Sicherheitsgruppe in Active Directory      |
| `06_user_added_to_group.png`            | User added to the correct security group / Benutzer zur richtigen Sicherheitsgruppe hinzugefügt |
| `07_access_test_successful.png`         | Successful access test / Erfolgreicher Zugriffstest                                             |
| `08_access_denied_test.png`             | Access denied test / Zugriff-verweigert-Test                                                    |

Screenshots are stored in:

Screenshots befinden sich im Ordner:

```text
evidence/02_File_Server_Access_Control/
```

or / oder:

```text
Beweis/02_Dateiserver-Zugriffskontrolle/
```

---

## Skills Demonstrated / Nachgewiesene Kompetenzen

This module demonstrates the following IT Administrator skills:

Dieses Modul zeigt folgende IT-Administrator-Kompetenzen:

* Windows File Server Administration
  Windows-Dateiserver-Administration

* SMB Share Configuration
  SMB-Freigabekonfiguration

* NTFS Permission Management
  Verwaltung von NTFS-Berechtigungen

* Active Directory Security Groups
  Active-Directory-Sicherheitsgruppen

* User and Group Management
  Benutzer- und Gruppenverwaltung

* Role-Based Access Control
  Rollenbasierte Zugriffskontrolle

* Least Privilege
  Least-Privilege-Prinzip

* Troubleshooting Access Issues
  Fehlerbehebung bei Zugriffsproblemen

* File Server Access Validation
  Validierung von Dateiserver-Zugriffen

---

## Business Relevance / Praxisrelevanz

In enterprise environments, file servers are commonly used to provide centralized access to department data.

In Unternehmensumgebungen werden Dateiserver häufig genutzt, um zentralen Zugriff auf Abteilungsdaten bereitzustellen.

This configuration helps IT teams to:

Diese Konfiguration hilft IT-Teams dabei:

* manage access centrally
  Zugriffe zentral zu verwalten

* protect sensitive department data
  sensible Abteilungsdaten zu schützen

* simplify onboarding and offboarding
  Onboarding und Offboarding zu vereinfachen

* reduce unauthorized access
  unberechtigte Zugriffe zu reduzieren

* support compliance and audit requirements
  Compliance- und Audit-Anforderungen zu unterstützen

---

## Result / Ergebnis

A central Windows File Server was successfully configured with department-based access control.

Ein zentraler Windows-Dateiserver wurde erfolgreich mit abteilungsbasierter Zugriffskontrolle eingerichtet.

Access to shared folders was controlled using Active Directory security groups, SMB shares, and NTFS permissions.

Der Zugriff auf freigegebene Ordner wurde über Active-Directory-Sicherheitsgruppen, SMB-Freigaben und NTFS-Berechtigungen gesteuert.

The access test confirmed that authorized users could access their department folder, while unauthorized users were denied access.

Der Zugriffstest bestätigte, dass berechtigte Benutzer auf ihren Abteilungsordner zugreifen konnten, während nicht berechtigte Benutzer keinen Zugriff erhielten.
