# 04 Backup and Restore / Backup und Wiederherstellung

## Project Overview / ProjektÃ¼bersicht

This module documents the implementation of backup and restore procedures using Veeam Backup & Replication and Windows Server Backup in a virtual enterprise IT lab environment.

Dieses Modul dokumentiert die Implementierung von Backup- und Restore-Prozessen mit Veeam Backup & Replication und Windows Server Backup in einer virtuellen Unternehmens-IT-Lab-Umgebung.

The objective was to demonstrate a practical understanding of backup strategies, scheduling, restore validation, and disaster recovery documentation â essential skills for any IT Administrator or System Administrator role.

Ziel war es, ein praxisnahes VerstÃ¤ndnis von Backup-Strategien, Zeitplanung, Restore-Validierung und Disaster-Recovery-Dokumentation zu zeigen â unverzichtbare Kenntnisse fÃ¼r jede IT-Administrator- oder Systemadministrator-Rolle.

---

## Lab Environment / Lab-Umgebung

* Windows Server 2022 (source system / Quellsystem)
* Veeam Backup & Replication (Community Edition)
* Windows Server Backup (built-in)
* Oracle VirtualBox
* VirtualBox shared folder or second virtual disk (backup target)
* Domain / DomÃ¤ne: `grclab.local`
* Server Name / Servername: `WIN-JTS1CJ3NE68`
* Backup Repository: Local folder or secondary virtual disk

---

## Project Goal / Projektziel

The goal of this module was to configure a reliable backup solution, validate restore procedures, and document the full backup lifecycle as operational evidence.

Ziel dieses Moduls war es, eine zuverlÃ¤ssige Backup-LÃ¶sung zu konfigurieren, Restore-Verfahren zu validieren und den gesamten Backup-Lebenszyklus als operativen Nachweis zu dokumentieren.

Expected result / Erwartetes Ergebnis:

```text
Backup job created and scheduled
Backup completed successfully
Test file deleted (simulated data loss)
File restored from backup
Restore validated â file available again
```

---

## Implemented Tasks / Umgesetzte Aufgaben

* Installed Veeam Backup & Replication Community Edition
  Veeam Backup & Replication Community Edition installiert

* Created backup repository on secondary storage
  Backup-Repository auf SekundÃ¤rspeicher erstellt

* Configured file-level backup job for Windows Server
  Datei-Level-Backup-Job fÃ¸r Windows Server konfiguriert

* Scheduled backup jobs (daily)
  Backup-Jobs geplant (tÃ¤glich)

* Ran manual backup job and confirmed completion
  Manuellen Backup-Job ausgefÃ¸hrt und erfolgreichen Abschluss bestÃ¤tigt

* Performed file-level restore test
  Datei-Level-Restore-Test durchgefÃ¸hrt

* Validated restore success
  Erfolgreiches Restore validiert

* Documented backup and restore process as operational evidence
  Backup- und Restore-Prozess als operativen Nachweis dokumentiert

---

## Backup Strategy / Backup-Strategie

The backup strategy follows the 3-2-1 backup principle as a conceptual baseline:

Die Backup-Strategie folgt dem 3-2-1-Backup-Prinzip als konzeptionelle Grundlage:

```text
3 copies of data
2 different storage media
1 copy offsite (simulated in lab with secondary virtual disk)
```

```text
3 Kopien der Daten
2 verschiedene Speichermedien
1 Kopie extern (im Lab mit sekundÃ¤rer virtueller Festplatte simuliert)
```

---

## Veeam Backup Configuration / Veeam-Backup-Konfiguration

### Backup Repository / Backup-Repository

```text
Repository Type:    Local folder / secondary virtual disk
Path:               D:\VeeamBackups
Concurrent tasks:   2
```

### Backup Job Settings / Backup-Job-Einstellungen

```text
Job Name:           WIN-Server-Daily-Backup
Backup Mode:        File-level backup
Source:             WIN-JTS1CJ3NE68 â C:\CompanyShares
Schedule:           Daily at 02:00
Restore Points:     14 (2 weeks retention)
Compression:        Optimal
```

---

## Backup Test Scenario / Backup-Testszenario

The following test scenario was used to validate the backup and restore process:

Folgendes Testszenario wurde verwendet, um den Backup- und Restore-Prozess zu validieren:

### Step 1: Create test file / Testdatei erstellen

```powershell
New-Item -Path "C:\CompanyShares\HR\backup_test.txt" -ItemType File
Set-Content -Path "C:\CompanyShares\HR\backup_test.txt" -Value "Backup test file - $(Get-Date)"
```

### Step 2: Run backup job / Backup-Job ausfÃ¼hren

```text
Veeam Backup & Replication â Jobs â WIN-Server-Daily-Backup â Start
```

### Step 3: Delete test file / Testdatei lÃ¶schen

```powershell
Remove-Item -Path "C:\CompanyShares\HR\backup_test.txt" -Force
```

### Step 4: Restore from backup / Aus Backup wiederherstellen

```text
Veeam â Home â Restore â File-Level Restore
Select backup point â Browse â HR â backup_test.txt â Restore to original location
```

### Step 5: Validate recovery / Wiederherstellung validieren

```powershell
Test-Path "C:\CompanyShares\HR\backup_test.txt"
```

Expected result / Erwartetes Ergebnis:

```text
True
```

---

## Windows Server Backup (Secondary Method) / Windows Server Backup (Zusatzmethode)

Windows Server Backup was also configured as a secondary backup method:

Windows Server Backup wurde zusÃ¤tzlich als sekundÃ¤re Backup-Methode konfiguriert:

```text
Feature:            Windows Server Backup (built-in)
Schedule:           Weekly on Sunday at 03:00
Backup Target:      Network share or secondary disk
Backup Type:        System state and critical volumes
```

Command to trigger manual backup:

Befehl fÃ¼r manuellen Backup:

```cmd
wbadmin start backup -backupTarget:D: -include:C: -allCritical -quiet
```

---

## Restore Procedure / Restore-Verfahren

### File-Level Restore via Veeam / Datei-Level-Restore Ã¼ber Veeam

```text
1. Open Veeam Backup & Replication
2. Home â Restore â Guest files (Windows)
3. Select backup job and restore point
4. Browse to file or folder location
5. Right-click â Restore to original location
6. Confirm overwrite if prompted
7. Validate file presence and content
```

### System State Restore via Windows Server Backup / System-State-Restore Ã¸ber Windows Server Backup

```text
1. Boot from Windows Server installation media
2. Select Repair your computer
3. System Image Recovery
4. Select latest backup
5. Confirm restore and restart
```

---

## Validation Summary / ValidierungsÃ¼bersicht

| Test | Expected Result | Status |
|------|----------------|--------|
| Backup repository created | Repository visible in Veeam | Completed |
| Backup job configured | Job listed in Veeam Jobs | Completed |
| Manual backup run | Job completed successfully | Completed |
| Test file created | File exists before backup | Completed |
| Test file deleted | File no longer exists | Completed |
| File-level restore | File restored to original location | Completed |
| Restore validation | File accessible and readable | Completed |

---

## Backup Retention Policy / Backup-Aufbewahrungsrichtlinie

```text
Daily backups:      14 restore points (2 weeks)
Weekly backups:     4 restore points (1 month)
Monthly backups:    3 restore points (3 months)
```

This ensures a granular restore capability while managing storage consumption.

Dies gewÃ¤hrleistet eine granulare WiederherstellungsmÃ¶glichkeit bei gleichzeitiger Kontrolle des Speicherverbrauchs.

---

## Troubleshooting / Fehlerbehebung

### Backup job fails â insufficient permissions / Backup-Job schlÃ¤gt fehl â unzureichende Berechtigungen

Resolution / LÃ¶sung:

```text
Ensure Veeam service account has administrator rights on the source machine
Veeam-Dienstkonto muss Administratorrechte auf dem Quellsystem haben
```

### Restore fails â backup file locked / Restore schlÃ¤gt fehl â Backup-Datei gesperrt

Resolution / LÃ¶sung:

```cmd
net stop veeambackupsvc
net start veeambackupsvc
```

### Not enough disk space for backup / Nicht genug Speicherplatz fÃ¼r Backup

Resolution / LÃ¶sung:

```text
Reduce restore points or add additional backup storage
Restore Points reduzieren oder zusÃ¤tzlichen Backup-Speicher hinzufÃ¼gen
```

---

## Evidence / Screenshots / Nachweise

| Screenshot | Description / Beschreibung |
|------------|---------------------------|
| `01_veeam_installation.png` | Veeam installation completed / Veeam-Installation abgeschlossen |
| `02_backup_repository.png` | Backup repository configuration / Konfiguration des Backup-Repositorys |
| `03_backup_job_config.png` | Backup job settings / Backup-Job-Einstellungen |
| `04_backup_job_running.png` | Backup job in progress / Laufender Backup-Job |
| `05_backup_job_success.png` | Backup completed successfully / Backup erfolgreich abgeschlossen |
| `06_test_file_created.png` | Test file created before backup / Testdatei vor dem Backup erstellt |
| `07_test_file_deleted.png` | Test file deleted (simulated loss) / Testdatei gelÃ¶scht (simulierter Datenverlust) |
| `08_veeam_file_restore.png` | File-level restore process / Datei-Level-Restore-Prozess |
| `09_restore_success.png` | Restored file visible in file explorer / Wiederhergestellte Datei im Datei-Explorer |
| `10_windows_server_backup.png` | Windows Server Backup configuration / Windows-Server-Backup-Konfiguration |

Screenshots are stored in:

```text
evidence/04_Backup_and_Restore/
```

---

## Skills Demonstrated / Nachgewiesene Kompetenzen

* Veeam Backup & Replication installation and configuration
* Backup repository setup / Backup-Repository-Einrichtung
* Backup job creation and scheduling / Backup-Job-Erstellung und -Planung
* File-level backup and restore / Datei-Level-Backup und -Restore
* Restore point management / Verwaltung von Restore-Punkten
* Windows Server Backup (wbadmin) / Windows Server Backup
* Backup retention policy design / Entwurf von Backup-Aufbewahrungsrichtlinien
* 3-2-1 backup strategy awareness / Kenntnis der 3-2-1-Backup-Strategie
* Disaster recovery planning / Disaster-Recovery-Planung
* Operational documentation / Operative Dokumentation

---

## Business Relevance / Praxisrelevanz

Backup and recovery is a critical requirement for every IT environment. Data loss from hardware failure, ransomware, or accidental deletion can be catastrophic without tested backup procedures.

Backup und Wiederherstellung sind eine kritische Anforderung in jeder IT-Umgebung. Datenverlust durch Hardwareausfall, Ransomware oder versehentliches LÃ¶schen kann ohne getestete Backup-Verfahren katastrophale Folgen haben.

This module demonstrates the ability to:

Dieses Modul demonstriert die FÃ¤higkeit:

* implement an enterprise backup solution
  eine unternehmensweite Backup-LÃ¶sung zu implementieren

* create and schedule automated backup jobs
  automatisierte Backup-Jobs zu erstellen und zu planen

* test and validate restore procedures
  Restore-Verfahren zu testen und zu validieren

* document operational procedures as audit evidence
  operative Verfahren als Audit-Nachweis zu dokumentieren

* design a basic backup retention policy
  eine grundlegende Backup-Aufbewahrungsrichtlinie zu entwerfen

---

## Result / Ergebnis

A functional backup solution was configured using Veeam Backup & Replication. Backup jobs were created, scheduled, and successfully executed. The restore procedure was tested and validated through a practical file deletion and recovery scenario. All steps were documented as operational evidence.

Eine funktionsfÃ¤hige Backup-LÃ¶sung wurde mit Veeam Backup & Replication konfiguriert. Backup-Jobs wurden erstellt, geplant und erfolgreich ausgefÃ¼hrt. Das Restore-Verfahren wurde durch ein praktisches Szenario mit DateilÃ¶schung und -wiederherstellung getestet und validiert. Alle Schritte wurden als operativer Nachweis dokumentiert.

This module demonstrates practical Disaster Recovery and Backup Administration skills applicable to enterprise IT environments.

Dieses Modul zeigt praxisnahe Disaster-Recovery- und Backup-Administrationskenntnisse, die in unternehmensweiten IT-Umgebungen anwendbar sind.
