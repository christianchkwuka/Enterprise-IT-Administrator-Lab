# 03 GPO Drive Mapping / GPO-Laufwerkszuordnung

## Project Overview / Projektübersicht

This module documents the configuration of automatic network drive mapping using Group Policy in a Windows Server Active Directory environment.

Dieses Modul dokumentiert die automatische Netzlaufwerkszuordnung über Gruppenrichtlinien in einer Windows-Server-Active-Directory-Umgebung.

The objective was to automatically map a department-based shared folder to a user through Group Policy Preferences. In this case, the HR shared folder was mapped as drive `H:` for an HR test user.

Ziel war es, einem Benutzer automatisch ein abteilungsbezogenes Netzlaufwerk über Group Policy Preferences bereitzustellen. In diesem Fall wurde der HR-Ordner als Laufwerk `H:` für einen HR-Testbenutzer verbunden.

---

## Lab Environment / Lab-Umgebung

* Windows Server 2022
* Active Directory Domain Services
* Group Policy Management Console
* Windows File Server
* SMB Share / SMB-Freigabe
* NTFS Permissions / NTFS-Berechtigungen
* Domain / Domäne: `grclab.local`
* Server Name / Servername: `WIN-JTS1CJ3NE68`
* Test User / Testbenutzer: `grclab\Friedrich.helmut`
* Shared Folder / Freigegebener Ordner: `\\WIN-JTS1CJ3NE68\HR`
* Mapped Drive Letter / Laufwerksbuchstabe: `H:`

---

## Project Goal / Projektziel

The goal of this module was to configure and validate automatic drive mapping for an HR user.

Ziel dieses Moduls war es, eine automatische Laufwerkszuordnung für einen HR-Benutzer zu konfigurieren und zu validieren.

Expected result / Erwartetes Ergebnis:

```text
HR (\\WIN-JTS1CJ3NE68\HR) (H:)
```

---

## Implemented Tasks / Umgesetzte Aufgaben

* Opened Group Policy Management Console
  Group Policy Management Console geöffnet

* Created a new Group Policy Object for HR drive mapping
  Neue Gruppenrichtlinie für die HR-Laufwerkszuordnung erstellt

* Linked the GPO to the HR Organizational Unit
  GPO mit der HR-Organizational Unit verknüpft

* Configured Drive Maps under User Configuration
  Drive Maps unter Benutzerkonfiguration eingerichtet

* Mapped the HR shared folder to drive letter `H:`
  HR-Freigabe als Laufwerk `H:` verbunden

* Forced Group Policy update using `gpupdate /force`
  Gruppenrichtlinienaktualisierung mit `gpupdate /force` erzwungen

* Verified applied policies using `gpresult /r`
  Angewendete Richtlinien mit `gpresult /r` geprüft

* Confirmed the mapped drive in File Explorer
  Netzlaufwerk im Datei-Explorer bestätigt

---

## GPO Configuration Path / GPO-Konfigurationspfad

The mapped drive was configured under:

Das Netzlaufwerk wurde unter folgendem Pfad konfiguriert:

```text
User Configuration
→ Preferences
→ Windows Settings
→ Drive Maps
```

This path is used because drive mapping is a user-based configuration. The network drive should follow the user, not the computer.

Dieser Pfad wird verwendet, weil die Laufwerkszuordnung benutzerbezogen ist. Das Netzlaufwerk soll dem Benutzer folgen, nicht dem Computer.

---

## Drive Mapping Configuration / Konfiguration der Laufwerkszuordnung

The following settings were used:

Folgende Einstellungen wurden verwendet:

```text
Action: Create
Location: \\WIN-JTS1CJ3NE68\HR
Drive Letter: H:
Label: HR Shared Drive
Reconnect: Enabled
```

The drive was mapped to the HR shared folder hosted on the Windows Server.

Das Laufwerk wurde mit dem HR-Freigabeordner auf dem Windows Server verbunden.

---

## GPO Linking / GPO-Verknüpfung

The Group Policy Object was linked to the HR Organizational Unit.

Die Gruppenrichtlinie wurde mit der HR-Organizational Unit verknüpft.

Example / Beispiel:

```text
OU: HR
GPO: Map_HR_Drive
```

This ensures that users inside the HR OU receive the HR network drive automatically.

Dadurch erhalten Benutzer innerhalb der HR-OU automatisch das HR-Netzlaufwerk.

---

## Validation Commands / Validierungsbefehle

### Force Group Policy Update / Gruppenrichtlinie aktualisieren

The following command was used to force Group Policy processing:

Folgender Befehl wurde verwendet, um die Gruppenrichtlinienverarbeitung zu erzwingen:

```cmd
gpupdate /force
```

Expected result / Erwartetes Ergebnis:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

---

### Check Applied Group Policies / Angewendete Gruppenrichtlinien prüfen

The following command was used to verify that the GPO was applied:

Folgender Befehl wurde verwendet, um zu prüfen, ob die GPO angewendet wurde:

```cmd
gpresult /r
```

Expected result / Erwartetes Ergebnis:

```text
Applied Group Policy Objects:
Map_HR_Drive
```

---

## Manual Network Drive Test / Manueller Netzlaufwerk-Test

To confirm that the share was reachable, the following command was also used:

Um zu prüfen, ob die Freigabe erreichbar ist, wurde zusätzlich folgender Befehl verwendet:

```cmd
net use H: \\WIN-JTS1CJ3NE68\HR /user:grclab\Friedrich.helmut
```

After successful authentication, the HR network drive was visible in File Explorer.

Nach erfolgreicher Authentifizierung war das HR-Netzlaufwerk im Datei-Explorer sichtbar.

---

## Troubleshooting / Fehlerbehebung

During the validation process, several typical issues were checked.

Während der Validierung wurden mehrere typische Fehler geprüft.

### Error: System error 86 / Fehler: Systemfehler 86

```text
The specified network password is not correct.
```

Cause / Ursache:

* Incorrect password was entered for the test user.
  Für den Testbenutzer wurde ein falsches Passwort eingegeben.

Resolution / Lösung:

* Verified and reset the user password in Active Directory Users and Computers.
  Das Benutzerpasswort wurde in Active Directory Users and Computers geprüft und zurückgesetzt.

---

### Error: System error 67 / Fehler: Systemfehler 67

```text
The network name cannot be found.
```

Cause / Ursache:

* Incorrect network path or missing share name.
  Falscher Netzwerkpfad oder fehlender Freigabename.

Resolution / Lösung:

* Verified the correct server name and share path.
  Servername und Freigabepfad wurden geprüft.

* Confirmed that the HR share existed on the server.
  Es wurde bestätigt, dass die HR-Freigabe auf dem Server existiert.

---

### Error: System error 85 / Fehler: Systemfehler 85

```text
The local device name is already in use.
```

Cause / Ursache:

* Drive letter `H:` was already mapped or reserved.
  Der Laufwerksbuchstabe `H:` war bereits verbunden oder reserviert.

Resolution / Lösung:

```cmd
net use H: /delete /y
```

or / oder:

```cmd
net use * /delete /y
```

After removing the existing mapping, the drive mapping was tested again.

Nach dem Entfernen der bestehenden Zuordnung wurde die Laufwerkszuordnung erneut getestet.

---

## Final Validation / Abschließende Validierung

The mapped network drive was successfully visible in File Explorer under **This PC**.

Das verbundene Netzlaufwerk war erfolgreich im Datei-Explorer unter **This PC / Dieser PC** sichtbar.

Final result / Endergebnis:

```text
HR (\\WIN-JTS1CJ3NE68\HR) (H:)
```

This confirms that the drive mapping configuration was successful.

Dies bestätigt, dass die Laufwerkszuordnung erfolgreich konfiguriert wurde.

---

## Evidence / Screenshots / Nachweise

The following screenshots document the implementation and validation process.

Die folgenden Screenshots dokumentieren die Umsetzung und Validierung.

| Screenshot                        | Description / Beschreibung                                                                                                |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `01_group_policy_management.png`  | Group Policy Management Console overview / Übersicht der Group Policy Management Console                                  |
| `02_create_gpo_map_hr_drive.png`  | Creation of the HR drive mapping GPO / Erstellung der HR-Laufwerks-GPO                                                    |
| `03_gpo_linked_to_hr_ou.png`      | GPO linked to the HR Organizational Unit / GPO mit der HR-OU verknüpft                                                    |
| `04_drive_maps_configuration.png` | Drive Maps configuration using Group Policy Preferences / Drive-Maps-Konfiguration über Group Policy Preferences          |
| `05_gpupdate_force.png`           | Manual policy update using `gpupdate /force` / Manuelle Richtlinienaktualisierung mit `gpupdate /force`                   |
| `06_gpresult_applied_gpo.png`     | Validation of applied Group Policy using `gpresult /r` / Prüfung der angewendeten GPO mit `gpresult /r`                   |
| `07_mapped_drive_visible.png`     | Successfully mapped HR network drive visible in File Explorer / Erfolgreich verbundenes HR-Netzlaufwerk im Datei-Explorer |

Screenshots are stored in:

Screenshots befinden sich im Ordner:

```text
evidence/03_GPO_Drive_Mapping/
```

or / oder:

```text
Beweis/03_GPO_Laufwerkszuordnung/
```

---

## Skills Demonstrated / Nachgewiesene Kompetenzen

This module demonstrates the following IT Administrator skills:

Dieses Modul zeigt folgende IT-Administrator-Kompetenzen:

* Group Policy Management / Gruppenrichtlinienverwaltung
* Active Directory Administration / Active-Directory-Administration
* GPO Drive Mapping / GPO-Laufwerkszuordnung
* File Server Administration / File-Server-Administration
* SMB Share Access / Zugriff auf SMB-Freigaben
* NTFS and Share Permission Awareness / Verständnis von NTFS- und Share-Berechtigungen
* User-based policy configuration / Benutzerbasierte Richtlinienkonfiguration
* Troubleshooting Group Policy issues / Fehlerbehebung bei Gruppenrichtlinien
* Command-line validation using `gpupdate`, `gpresult`, and `net use`
  Validierung über Kommandozeile mit `gpupdate`, `gpresult` und `net use`
* Enterprise-style user access provisioning / Benutzerzugriff in einer unternehmensnahen Umgebung

---

## Business Relevance / Praxisrelevanz

In enterprise environments, mapped drives are commonly used to provide users with structured access to department-specific file shares.

In Unternehmensumgebungen werden Netzlaufwerke häufig verwendet, um Benutzern strukturierten Zugriff auf abteilungsspezifische Freigaben bereitzustellen.

This configuration helps IT teams to:

Diese Konfiguration hilft IT-Teams dabei:

* automate access to shared folders
  Zugriff auf freigegebene Ordner zu automatisieren

* reduce manual configuration effort
  manuelle Konfigurationsarbeit zu reduzieren

* improve user onboarding
  Benutzer-Onboarding zu verbessern

* enforce department-based access control
  abteilungsbasierte Zugriffskontrolle umzusetzen

* support centralized file management
  zentrale Dateiverwaltung zu unterstützen

* simplify troubleshooting and documentation
  Fehlerbehebung und Dokumentation zu vereinfachen

---

## Result / Ergebnis

The HR network drive was successfully mapped as drive `H:` using Group Policy Drive Mapping. The configuration was validated through Group Policy update, policy result checking, manual network drive testing, and confirmation in File Explorer.

Das HR-Netzlaufwerk wurde erfolgreich als Laufwerk `H:` über Group Policy Drive Mapping verbunden. Die Konfiguration wurde durch Gruppenrichtlinienaktualisierung, Prüfung der angewendeten Richtlinien, manuellen Netzlaufwerk-Test und Bestätigung im Datei-Explorer validiert.

This module successfully demonstrates a practical enterprise IT administration task involving Active Directory, Group Policy, File Server access, and user-based resource provisioning.

Dieses Modul zeigt erfolgreich eine praxisnahe IT-Administrationsaufgabe mit Active Directory, Gruppenrichtlinien, File-Server-Zugriff und benutzerbasierter Bereitstellung von Ressourcen.
