# 07 Monitoring, Logs & ISMS

## Project Overview / ProjektÃ¼bersicht

This module documents the implementation of infrastructure monitoring, log collection, and ISMS evidence generation using Checkmk and Wazuh in a virtual enterprise IT lab environment.

Dieses Modul dokumentiert die Implementierung von Infrastrukturmonitoring, Protokollsammlung und ISMS-Nachweisen mit Checkmk und Wazuh in einer virtuellen Unternehmens-IT-Lab-Umgebung.

---

## Lab Environment / Lab-Umgebung

* Ubuntu Server 22.04 (Checkmk and Wazuh host)
* Windows Server 2022 (monitored system)
* Checkmk Raw Edition (open source)
* Wazuh SIEM / XDR (open source)
* Oracle VirtualBox
* Monitoring Server IP: `192.168.56.24`
* Windows Server IP: `192.168.56.26`
* Checkmk agent port: `6556`
* Wazuh agent port: `1514` (UDP)

---

## Implemented Tasks / Umgesetzte Aufgaben

* Installed Checkmk Raw Edition on Ubuntu Server
* Created Checkmk monitoring site 'grclab'
* Installed Checkmk agent on Windows Server (port 6556)
* Added Windows Server as monitored host in Checkmk
* Discovered services and activated monitoring
* Installed Wazuh Manager on Ubuntu
* Installed Wazuh agent on Windows Server
* Validated log collection and alert generation
* Collected ISMS evidence from both tools

---

## Checkmk Installation & Configuration

```bash
# Install Checkmk Raw Edition
wget https://download.checkmk.com/checkmk/2.2.0p20/check-mk-raw-2.2.0p20_0.jammy_amd64.deb
sudo apt install ./check-mk-raw-2.2.0p20_0.jammy_amd64.deb

# Create monitoring site
omd create grclab
omd start grclab
```

### Access Web Interface

```text
URL:      http://192.168.56.24/grclab
Username: cmkadmin
```

### Add Windows Server as Monitored Host

```text
Setup â Hosts â Add Host
Host name:    WIN-JTS1CJ3NE68
IP Address:   192.168.56.26
Agent:        Checkmk Agent (port 6556)
```

Discovered services included:

```text
CPU usage, Memory usage, Disk space
Windows services, Event log monitoring
Network interfaces, Uptime
```

---

## Wazuh Installation & Configuration

```bash
# Install Wazuh repository and manager
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring \
    --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import

apt-get update && apt-get install wazuh-manager
systemctl enable --now wazuh-manager
```

### Install Wazuh Agent on Windows Server

```powershell
msiexec.exe /i wazuh-agent-4.7.0-1.msi /q WAZUH_MANAGER="192.168.56.24" `
    WAZUH_AGENT_NAME="WIN-JTS1CJ3NE68"
NET START WazuhSvc
```

---

## Monitored Security Events / Ereignisse

Wazuh monitors Windows Security, System, and Application event logs:

| Event ID | Description |
|----------|-------------|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4634 | Logoff |
| 4720 | User account created |
| 4740 | Account lockout |
| 4776 | Credential validation |

---

## ISMS Evidence Collection

| Evidence Type | Tool | Description |
|---------------|------|-------------|
| System health status | Checkmk | All hosts green / services monitored |
| Failed login attempts | Wazuh | Event ID 4625 alerts logged |
| Account lockout events | Wazuh | Event ID 4740 alerts captured |
| Service availability | Checkmk | Uptime monitoring for all hosts |
| Disk space monitoring | Checkmk | Threshold alerts configured |

---

## Checkmk Alert Thresholds

```text
CPU usage:    WARNING at 80%, CRITICAL at 95%
Memory usage: WARNING at 85%, CRITICAL at 95%
Disk space:   WARNING at 80%, CRITICAL at 90%
Service down: CRITICAL immediately
```

---

## Validation / Validierung

```bash
# Check Wazuh agent status
/var/ossec/bin/agent_control -l
# Expected: ID: 001, Name: WIN-JTS1CJ3NE68, Status: Active
```

```text
Checkmk Dashboard: All hosts UP, all services OK
Wazuh: Agent connected, security alerts firing for Events 4625 and 4740
```

---

## Skills Demonstrated / Nachgewiesene Kompetenzen

* Checkmk installation, site management, host monitoring
* Windows and Linux agent deployment
* Service discovery and threshold alerting
* Wazuh SIEM installation and configuration
* Windows Security event log monitoring
* ISMS evidence collection and documentation
* Alert analysis and security event detection

---

## Result / Ergebnis

A complete monitoring and log analysis environment was successfully deployed using Checkmk for infrastructure monitoring and Wazuh for SIEM and security event detection. All lab systems were monitored, security events logged and alerted, and ISMS evidence collected.

Eine vollstÃ¤ndige Monitoring- und Log-Analyse-Umgebung wurde erfolgreich bereitgestellt. Alle Lab-Systeme wurden Ã¼berwacht, Sicherheitsereignisse protokolliert und ISMS-Nachweise gesammelt.
