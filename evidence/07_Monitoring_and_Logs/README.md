
# 07 Monitoring and Logs

## Projektziel

In diesem Modul wurde die Überwachung von Windows-Server-, Active-Directory-, Backup- und Netzwerkereignissen dokumentiert. Ziel war es, typische Monitoring- und Logging-Aufgaben eines IT-Administrators praktisch nachzuvollziehen.

## Umgebung

- Windows Server 2022
- Active Directory Domain Services
- Windows Event Viewer
- Windows Server Backup
- Group Policy
- pfSense Firewall
- Optional: Wazuh SIEM
- Domäne: `grclab.local`

## Umgesetzte Aufgaben

- Überprüfung von Windows Server Ereignisprotokollen
- Analyse von Active-Directory- und Anmeldeereignissen
- Überprüfung fehlgeschlagener Anmeldeversuche
- Prüfung von Backup-Ereignissen
- Überwachung von Gruppenrichtlinienereignissen
- Analyse von pfSense Firewall Logs
- Dokumentation typischer IT-Events und Fehlerquellen
- Optional: Weiterleitung von Logs an Wazuh SIEM

## Warum Monitoring wichtig ist

Monitoring hilft IT-Administratoren dabei, Probleme frühzeitig zu erkennen, Sicherheitsereignisse zu analysieren und die Stabilität der IT-Umgebung sicherzustellen.

Typische Ziele:

- Fehler schneller erkennen
- Sicherheitsvorfälle nachvollziehen
- Systemverfügbarkeit überwachen
- Backup-Status prüfen
- Anmeldeprobleme analysieren
- Netzwerkzugriffe kontrollieren
- Audit- und Compliance-Anforderungen unterstützen

## Windows Event Viewer

Der Windows Event Viewer wird genutzt, um System-, Sicherheits- und Anwendungsereignisse zu prüfen.

Pfad:

```text
Server Manager
→ Tools
→ Event Viewer
