# 05 pfSense Network Segmentation / pfSense Netzwerksegmentierung

## Project Overview / Projektübersicht

This module documents the implementation of network segmentation using pfSense in a virtual enterprise IT lab environment.

Dieses Modul dokumentiert die Umsetzung einer Netzwerksegmentierung mit pfSense in einer virtuellen unternehmensnahen IT-Lab-Umgebung.

The goal was to separate different network areas such as HR, Finance, IT and DMZ, and to control communication between them using firewall rules.

Ziel war es, verschiedene Netzwerkbereiche wie HR, Finance, IT und DMZ voneinander zu trennen und die Kommunikation zwischen diesen Bereichen über Firewall-Regeln zu kontrollieren.

---

## Lab Environment / Lab-Umgebung

* pfSense Firewall
* Windows Server 2022
* Active Directory Domain Services
* Windows Client / Test Client
* Checkmk Monitoring Server
* VirtualBox
* Internal / Host-only Networks
* Multiple virtual network interfaces

---

## Project Goal / Projektziel

The objective of this module was to simulate a realistic enterprise network segmentation scenario.

Ziel dieses Moduls war es, ein realistisches Unternehmensszenario zur Netzwerksegmentierung nachzubilden.

The main goals were:

Die Hauptziele waren:

* Separate internal departments into different network segments
  Interne Abteilungen in verschiedene Netzwerksegmente trennen

* Control access between HR, Finance, IT and DMZ
  Zugriff zwischen HR, Finance, IT und DMZ kontrollieren

* Allow only required communication
  Nur notwendige Kommunikation erlauben

* Block unauthorized traffic between sensitive networks
  Nicht autorisierten Datenverkehr zwischen sensiblen Netzwerken blockieren

* Validate allowed and blocked traffic through ping tests and firewall logs
  Erlaubten und blockierten Datenverkehr mit Ping-Tests und Firewall-Logs validieren

---

## Network Segments / Netzwerksegmente

Example network segmentation:

Beispielhafte Netzwerksegmentierung:

```text
LAN       → Main internal network
HR        → Human Resources network
Finance   → Finance department network
IT        → IT administration network
DMZ       → Demilitarized zone for isolated systems
```

Beispiel:

```text
LAN       → Internes Hauptnetzwerk
HR        → Personalabteilung
Finance   → Finanzabteilung
IT        → IT-Administrationsnetzwerk
DMZ       → Demilitarisierte Zone für isolierte Systeme
```

---

## Why Network Segmentation Matters / Warum Netzwerksegmentierung wichtig ist

Network segmentation improves security by limiting communication between systems and departments.

Netzwerksegmentierung verbessert die Sicherheit, indem Kommunikation zwischen Systemen und Abteilungen eingeschränkt wird.

It helps to:

Sie hilft dabei:

* reduce lateral movement after a compromise
  laterale Bewegungen nach einem Angriff zu reduzieren

* protect sensitive systems and data
  sensible Systeme und Daten zu schützen

* separate high-risk areas such as DMZ from internal networks
  risikoreiche Bereiche wie die DMZ von internen Netzwerken zu trennen

* enforce least privilege communication
  Kommunikation nach dem Least-Privilege-Prinzip umzusetzen

* improve firewall visibility and auditability
  Transparenz und Nachvollziehbarkeit von Firewall-Regeln zu verbessern

---

## Implemented Tasks / Umgesetzte Aufgaben

The following tasks were completed:

Folgende Aufgaben wurden umgesetzt:

* Configured pfSense interfaces
  pfSense-Interfaces konfiguriert

* Created or assigned network segments
  Netzwerksegmente erstellt oder zugewiesen

* Configured firewall rules for HR, Finance, IT and DMZ
  Firewall-Regeln für HR, Finance, IT und DMZ konfiguriert

* Configured DHCP services for internal networks
  DHCP-Dienste für interne Netzwerke konfiguriert

* Allowed required traffic only
  Nur notwendigen Datenverkehr erlaubt

* Blocked unauthorized communication between networks
  Nicht autorisierte Kommunikation zwischen Netzwerken blockiert

* Reviewed firewall logs
  Firewall-Logs geprüft

* Validated allowed traffic with ping test
  Erlaubten Datenverkehr mit Ping-Test validiert

* Validated blocked traffic with ping test
  Blockierten Datenverkehr mit Ping-Test validiert

---

## pfSense Interfaces / pfSense-Interfaces

The pfSense firewall was configured with multiple interfaces for different network areas.

Die pfSense-Firewall wurde mit mehreren Interfaces für unterschiedliche Netzwerkbereiche konfiguriert.

Example:

```text
WAN
LAN
HR
Finance
IT
DMZ
```

Each interface represents a separate network zone.

Jedes Interface stellt eine eigene Netzwerkzone dar.

Evidence:

```text
01_pfsense_interfaces.png
```

---

## VLAN / Network Overview / VLAN- oder Netzwerkübersicht

Depending on the lab setup, segmentation can be implemented using VLANs or separate VirtualBox network adapters.

Je nach Lab-Aufbau kann die Segmentierung über VLANs oder separate VirtualBox-Netzwerkadapter umgesetzt werden.

In this lab, the network overview documents the logical separation of different network areas.

In diesem Lab dokumentiert die Netzwerkübersicht die logische Trennung verschiedener Netzwerkbereiche.

Evidence:

```text
02_vlan_overview.png
```

If VLAN tagging was not used, the following note applies:

Falls kein VLAN-Tagging verwendet wurde, gilt folgende Erklärung:

```text
This lab uses separate virtual interfaces instead of VLAN tagging due to VirtualBox lab limitations.
```

```text
Dieses Lab verwendet separate virtuelle Interfaces anstelle von VLAN-Tagging aufgrund der Einschränkungen der VirtualBox-Lab-Umgebung.
```

---

## Firewall Rule Concept / Firewall-Regelkonzept

The firewall rules were designed according to the principle of least privilege.

Die Firewall-Regeln wurden nach dem Least-Privilege-Prinzip entworfen.

This means:

Das bedeutet:

```text
Only required traffic is allowed.
All unnecessary traffic is blocked.
Sensitive networks are protected from unauthorized access.
```

```text
Nur notwendiger Datenverkehr wird erlaubt.
Nicht notwendiger Datenverkehr wird blockiert.
Sensible Netzwerke werden vor unberechtigtem Zugriff geschützt.
```

---

## HR Firewall Rules / HR-Firewall-Regeln

Example HR rules:

Beispielhafte HR-Regeln:

```text
Allow HR to DNS
Allow HR to required internal services
Allow HR to Internet if required
Block HR to Finance
Block HR to DMZ
```

Purpose:

Zweck:

HR users should access only required services and should not directly access Finance or DMZ resources.

HR-Benutzer sollen nur notwendige Dienste erreichen und keinen direkten Zugriff auf Finance- oder DMZ-Ressourcen erhalten.

Evidence:

```text
03_firewall_rules_hr.png
```

---

## Finance Firewall Rules / Finance-Firewall-Regeln

Example Finance rules:

Beispielhafte Finance-Regeln:

```text
Allow Finance to DNS
Allow Finance to required internal services
Block Finance to HR
Block Finance to DMZ
Block unnecessary traffic
```

Purpose:

Zweck:

The Finance network contains sensitive data and should be more restricted.

Das Finance-Netzwerk enthält sensible Daten und sollte stärker eingeschränkt sein.

Evidence:

```text
04_firewall_rules_finance.png
```

---

## IT Firewall Rules / IT-Firewall-Regeln

Example IT rules:

Beispielhafte IT-Regeln:

```text
Allow IT to Windows Server
Allow IT to pfSense management
Allow IT to Checkmk monitoring server
Allow IT to Veeam backup server
Allow IT to required administrative services
```

Purpose:

Zweck:

The IT network requires administrative access to infrastructure systems.

Das IT-Netzwerk benötigt administrativen Zugriff auf Infrastruktursysteme.

Evidence:

```text
05_firewall_rules_it.png
```

---

## DMZ Firewall Rules / DMZ-Firewall-Regeln

The DMZ was configured with a restrictive security policy.

Die DMZ wurde mit einer restriktiven Sicherheitsrichtlinie konfiguriert.

Example DMZ rules:

Beispielhafte DMZ-Regeln:

```text
Allow DMZ to Internet if needed
Block DMZ to LAN
Block DMZ to HR
Block DMZ to Finance
Block DMZ to Domain Controller
Allow only required ports
```

Recommended allowed outbound ports:

Empfohlene erlaubte ausgehende Ports:

```text
DNS 53
HTTP 80
HTTPS 443
```

Purpose:

Zweck:

DMZ systems should not freely communicate with internal networks. This reduces the risk of lateral movement if a DMZ system is compromised.

DMZ-Systeme sollen nicht frei mit internen Netzwerken kommunizieren dürfen. Dadurch wird das Risiko lateraler Bewegungen reduziert, falls ein DMZ-System kompromittiert wird.

Evidence:

```text
06_firewall_rules_dmz.png
```

---

## DHCP Configuration / DHCP-Konfiguration

DHCP was configured to provide automatic IP addressing for selected network segments.

DHCP wurde konfiguriert, um ausgewählten Netzwerksegmenten automatisch IP-Adressen bereitzustellen.

Example DHCP ranges:

Beispielhafte DHCP-Bereiche:

```text
HR       → 192.168.10.100 - 192.168.10.200
Finance  → 192.168.20.100 - 192.168.20.200
IT       → 192.168.30.100 - 192.168.30.200
DMZ      → 192.168.40.100 - 192.168.40.200
```

Evidence:

```text
07_dhcp_configuration.png
```

---

## Firewall Logs / Firewall-Logs

Firewall logs were reviewed to validate blocked traffic.

Firewall-Logs wurden geprüft, um blockierten Datenverkehr zu validieren.

pfSense path:

pfSense-Pfad:

```text
Status
→ System Logs
→ Firewall
```

The logs help identify:

Die Logs helfen bei der Analyse von:

```text
Source IP
Destination IP
Interface
Port
Protocol
Allowed or blocked action
Firewall rule match
```

Evidence:

```text
08_firewall_logs_blocked_traffic.png
```

---

## Allowed Ping Test / Erlaubter Ping-Test

An allowed ping test was performed to confirm that permitted communication works.

Ein erlaubter Ping-Test wurde durchgeführt, um zu bestätigen, dass erlaubte Kommunikation funktioniert.

Example:

Beispiel:

```cmd
ping 192.168.56.26
```

Expected result:

Erwartetes Ergebnis:

```text
Reply from 192.168.56.26
Packets: Sent = 4, Received = 4, Lost = 0
```

This confirms that traffic between the allowed source and destination is permitted by the firewall rules.

Dies bestätigt, dass der Datenverkehr zwischen erlaubter Quelle und erlaubtem Ziel durch die Firewall-Regeln zugelassen wird.

Evidence:

```text
09_ping_test_allowed.png
```

---

## Blocked Ping Test / Blockierter Ping-Test

A blocked ping test was performed to confirm that unauthorized communication is denied.

Ein blockierter Ping-Test wurde durchgeführt, um zu bestätigen, dass nicht autorisierte Kommunikation verweigert wird.

Example:

Beispiel:

```cmd
ping 192.168.20.10
```

Expected result:

Erwartetes Ergebnis:

```text
Request timed out
```

or:

```text
Destination host unreachable
```

This confirms that traffic between restricted networks is blocked by pfSense.

Dies bestätigt, dass Datenverkehr zwischen eingeschränkten Netzwerken durch pfSense blockiert wird.

Evidence:

```text
10_ping_test_blocked.png
```

---

## Validation Summary / Validierungsübersicht

| Test                          | Expected Result                     | Status    |
| ----------------------------- | ----------------------------------- | --------- |
| Interface configuration       | Interfaces visible in pfSense       | Completed |
| Network segmentation overview | Segments documented                 | Completed |
| HR firewall rules             | HR traffic controlled               | Completed |
| Finance firewall rules        | Finance traffic restricted          | Completed |
| IT firewall rules             | Administrative access allowed       | Completed |
| DMZ firewall rules            | DMZ isolated from internal networks | Completed |
| DHCP configuration            | Clients receive IP addresses        | Completed |
| Firewall logs                 | Blocked traffic visible             | Completed |
| Allowed ping test             | Ping successful                     | Completed |
| Blocked ping test             | Ping blocked                        | Completed |

---

## Skills Demonstrated / Nachgewiesene Kompetenzen

This module demonstrates the following IT Administrator skills:

Dieses Modul zeigt folgende IT-Administrator-Kompetenzen:

* pfSense firewall administration
  pfSense-Firewall-Administration

* Network segmentation
  Netzwerksegmentierung

* Firewall rule design
  Firewall-Regeldesign

* DHCP configuration
  DHCP-Konfiguration

* Basic routing understanding
  Grundverständnis von Routing

* DMZ security concept
  DMZ-Sicherheitskonzept

* Least privilege network access
  Netzwerkzugriff nach dem Least-Privilege-Prinzip

* Traffic validation using ping tests
  Validierung von Datenverkehr mit Ping-Tests

* Firewall log analysis
  Analyse von Firewall-Logs

* Troubleshooting network connectivity
  Fehlerbehebung bei Netzwerkverbindungen

---

## Business Relevance / Praxisrelevanz

In enterprise environments, network segmentation is used to separate departments, protect sensitive systems, and reduce the impact of security incidents.

In Unternehmensumgebungen wird Netzwerksegmentierung genutzt, um Abteilungen zu trennen, sensible Systeme zu schützen und die Auswirkungen von Sicherheitsvorfällen zu reduzieren.

This configuration helps IT teams to:

Diese Konfiguration hilft IT-Teams dabei:

* reduce lateral movement
  laterale Bewegungen zu reduzieren

* protect sensitive networks such as Finance and HR
  sensible Netzwerke wie Finance und HR zu schützen

* isolate DMZ systems from internal infrastructure
  DMZ-Systeme von interner Infrastruktur zu isolieren

* control communication between departments
  Kommunikation zwischen Abteilungen zu kontrollieren

* improve security monitoring and auditability
  Sicherheitsüberwachung und Nachvollziehbarkeit zu verbessern

---

## Evidence / Screenshots / Nachweise

The following screenshots document the implementation and validation process.

Die folgenden Screenshots dokumentieren die Umsetzung und Validierung.

| Screenshot                             | Description / Beschreibung                                                                     |
| -------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `01_pfsense_interfaces.png`            | pfSense interface overview / Übersicht der pfSense-Interfaces                                  |
| `02_vlan_overview.png`                 | VLAN or network segmentation overview / VLAN- oder Netzwerksegmentierungsübersicht             |
| `03_firewall_rules_hr.png`             | HR firewall rules / HR-Firewall-Regeln                                                         |
| `04_firewall_rules_finance.png`        | Finance firewall rules / Finance-Firewall-Regeln                                               |
| `05_firewall_rules_it.png`             | IT firewall rules / IT-Firewall-Regeln                                                         |
| `06_firewall_rules_dmz.png`            | DMZ firewall rules / DMZ-Firewall-Regeln                                                       |
| `07_dhcp_configuration.png`            | DHCP configuration / DHCP-Konfiguration                                                        |
| `08_firewall_logs_blocked_traffic.png` | Blocked traffic in firewall logs / Blockierter Datenverkehr in Firewall-Logs                   |
| `09_ping_test_allowed.png`             | Successful ping test for allowed traffic / Erfolgreicher Ping-Test für erlaubten Datenverkehr  |
| `10_ping_test_blocked.png`             | Failed ping test for blocked traffic / Fehlgeschlagener Ping-Test für blockierten Datenverkehr |

Screenshots are stored in:

Screenshots befinden sich im Ordner:

```text
evidence/05_pfSense_Network_Segmentation/
```

or / oder:

```text
Beweis/05_pfSense_Netzwerksegmentierung/
```

---

## Result / Ergebnis

The pfSense network segmentation lab was successfully documented and validated.

Das pfSense-Netzwerksegmentierungs-Lab wurde erfolgreich dokumentiert und validiert.

Firewall rules were used to control communication between HR, Finance, IT and DMZ networks. Allowed traffic was validated through a successful ping test, while restricted communication was validated through blocked ping tests and firewall logs.

Firewall-Regeln wurden verwendet, um die Kommunikation zwischen HR-, Finance-, IT- und DMZ-Netzwerken zu kontrollieren. Erlaubter Datenverkehr wurde durch einen erfolgreichen Ping-Test validiert, während eingeschränkte Kommunikation durch blockierte Ping-Tests und Firewall-Logs nachgewiesen wurde.

This module demonstrates practical knowledge of enterprise-style network segmentation, firewall rule management and network security validation using pfSense.

Dieses Modul zeigt praktische Kenntnisse in unternehmensnaher Netzwerksegmentierung, Firewall-Regelverwaltung und Validierung von Netzwerksicherheit mit pfSense.
