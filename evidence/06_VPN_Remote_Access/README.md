
# 06 VPN Remote Access

## Projektziel

In diesem Modul wurde ein VPN-Fernzugriffskonzept für eine Unternehmensumgebung dokumentiert. Ziel war es, externen Benutzern einen sicheren Zugriff auf interne Ressourcen zu ermöglichen und den Zugriff über Firewall-Regeln kontrolliert zu beschränken.

## Umgebung

- pfSense Firewall
- Windows Server 2022
- Active Directory
- File Server
- Interne Netzwerke / VLANs
- VPN-Client
- Virtuelle Lab-Umgebung

## Umgesetzte Aufgaben

- Planung eines sicheren VPN-Zugriffs
- Einrichtung eines VPN-Netzwerks
- Definition von VPN-Benutzern
- Zugriffsbeschränkung über Firewall-Regeln
- Test des Zugriffs auf interne Ressourcen
- Prüfung von erlaubtem und blockiertem Datenverkehr
- Dokumentation des VPN-Zugriffs

## Warum VPN wichtig ist

Ein VPN ermöglicht Benutzern den sicheren Zugriff auf interne Unternehmensressourcen, auch wenn sie sich außerhalb des Firmennetzwerks befinden.

Typische Anwendungsfälle:

- Homeoffice
- Zugriff auf interne Dateiserver
- Zugriff auf Administrationssysteme
- Support durch externe Dienstleister
- Sichere Verbindung zu Unternehmensnetzwerken

## VPN-Grundprinzip

Ein externer Benutzer verbindet sich über einen VPN-Client mit der Unternehmensfirewall. Nach erfolgreicher Authentifizierung erhält der Benutzer Zugriff auf definierte interne Ressourcen.

Beispiel:

```text
Remote User
→ VPN Client
→ pfSense VPN Gateway
→ Internal Network
→ File Server / Windows Server
