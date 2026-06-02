
# 03 GPO Drive Mapping

## Projektziel

In diesem Modul wurde eine automatische Netzlaufwerkszuordnung über Gruppenrichtlinien eingerichtet. Ziel war es, Benutzern je nach Abteilung automatisch das passende Netzlaufwerk bereitzustellen.

## Umgebung

- Windows Server 2022
- Active Directory Domain Services
- Group Policy Management
- File Server
- SMB-Freigaben
- Domäne: `grclab.local`

## Umgesetzte Aufgaben

- Erstellung einer Gruppenrichtlinie für Netzlaufwerke
- Verknüpfung der GPO mit der passenden Organizational Unit
- Konfiguration von Drive Maps über Group Policy Preferences
- Automatische Zuweisung von Laufwerksbuchstaben
- Test der Richtlinienanwendung mit einem Domänenbenutzer
- Validierung über `gpupdate /force` und Anmeldung am Client

## Beispielhafte Netzlaufwerke

```text
HR      → H: → \\WIN-JTS1CJ3NE68\HR
Finance → F: → \\WIN-JTS1CJ3NE68\Finance
IT      → I: → \\WIN-JTS1CJ3NE68\IT
Sales   → S: → \\WIN-JTS1CJ3NE68\Sales
