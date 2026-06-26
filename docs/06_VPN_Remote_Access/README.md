# 06 VPN Remote Access / VPN-Fernzugang

## Project Overview / ProjektÃ¼bersicht

This module documents the configuration of a secure VPN remote access solution using OpenVPN on pfSense. The goal was to simulate a realistic enterprise remote access scenario where administrators and users can securely connect to internal resources from outside the network.

Dieses Modul dokumentiert die Konfiguration einer sicheren VPN-FernzugangslÃ¶sung mit OpenVPN auf pfSense. Ziel war es, ein realistisches Enterprise-Fernzugangsszenario zu simulieren, bei dem Administratoren und Benutzer sich sicher von auÃerhalb des Netzwerks mit internen Ressourcen verbinden kÃ¶nnen.

---

## Lab Environment / Lab-Umgebung

* pfSense Firewall (version 2.7.x)
* OpenVPN (built into pfSense)
* Windows Client (OpenVPN Client)
* Windows Server 2022 (internal target)
* Oracle VirtualBox
* pfSense Web GUI: `192.168.56.100`
* Internal network: `192.168.56.0/24`
* VPN tunnel subnet: `10.8.0.0/24`

---

## Project Goal / Projektziel

The goal was to configure OpenVPN on pfSense to allow authenticated remote access to the internal lab network, and to validate the connection using a VPN client on Windows.

Ziel war es, OpenVPN auf pfSense zu konfigurieren, um authentifizierten Fernzugang zum internen Lab-Netzwerk zu ermÃ¶glichen und die Verbindung mit einem VPN-Client auf Windows zu validieren.

Expected result / Erwartetes Ergebnis:

```text
VPN client connects to pfSense OpenVPN server
Client receives IP from VPN tunnel subnet (10.8.0.x)
Client can reach internal resources (ping 192.168.56.26)
Traffic is encrypted through VPN tunnel
```

---

## Implemented Tasks / Umgesetzte Aufgaben

* Configured OpenVPN server on pfSense
  OpenVPN-Server auf pfSense konfiguriert

* Created CA (Certificate Authority) and server certificate
  CA (Zertifizierungsstelle) und Server-Zertifikat erstellt

* Created VPN user account and client certificate
  VPN-Benutzerkonto und Client-Zertifikat erstellt

* Configured firewall rules to allow VPN traffic
  Firewall-Regeln fÃ¼r VPN-Datenverkehr konfiguriert

* Exported OpenVPN client configuration (.ovpn)
  OpenVPN-Client-Konfiguration (.ovpn) exportiert

* Installed OpenVPN client on Windows
  OpenVPN-Client auf Windows installiert

* Connected to VPN and validated tunnel connectivity
  VPN-Verbindung hergestellt und Tunnel-KonnektivitÃ¤t validiert

* Tested access to internal resources through VPN
  Zugriff auf interne Ressourcen Ã¼ber VPN getestet

* Reviewed VPN connection logs
  VPN-Verbindungslogs Ã¼berprÃ¼ft

---

## Certificate Authority Setup / Zertifizierungsstelle einrichten

A Certificate Authority (CA) was created within pfSense Certificate Manager:

Eine Zertifizierungsstelle (CA) wurde im pfSense Certificate Manager erstellt:

```text
Path: System â Certificate Manager â CAs â Add

CA Name:        grclab-CA
Method:         Create an internal Certificate Authority
Key Length:     2048 bits
Digest:         SHA256
Lifetime:       3650 days (10 years)
Common Name:    grclab-CA
```

---

## Server Certificate / Server-Zertifikat

A server certificate was created and signed by the internal CA:

Ein Server-Zertifikat wurde erstellt und von der internen CA signiert:

```text
Path: System â Certificate Manager â Certificates â Add

Certificate Name:  openvpn-server
Certificate Type:  Server Certificate
CA:                grclab-CA
Key Length:        2048 bits
Digest:            SHA256
Lifetime:          3650 days
Common Name:       openvpn-server
```

---

## OpenVPN Server Configuration / OpenVPN-Server-Konfiguration

```text
Path: VPN â OpenVPN â Servers â Add

Server Mode:        Remote Access (SSL/TLS + User Auth)
Backend:            Local Database
Protocol:           UDP on IPv4 only
Device Mode:        tun (tunnel mode)
Interface:          WAN
Port:               1194
TLS Authentication: Enabled (tls-auth key generated)
Peer Certificate CA: grclab-CA
Server Certificate: openvpn-server
DH Parameter Length: 2048 bit
Encryption:         AES-256-GCM
Auth Digest:        SHA256
IPv4 Tunnel Network: 10.8.0.0/24
Redirect Gateway:   Enabled
DNS Default Domain: grclab.local
DNS Server 1:       192.168.56.26
Push Routes:        192.168.56.0/24
```

---

## VPN User Account / VPN-Benutzerkonto

A local user account was created for VPN authentication:

Ein lokales Benutzerkonto wurde fÃ¼r die VPN-Authentifizierung erstellt:

```text
Path: System â User Manager â Users â Add

Username:    vpn.admin
Password:    [strong password]
Certificate: [user certificate signed by grclab-CA]
```

A client certificate was also created for this user:

Ein Client-Zertifikat wurde fÃ¼r diesen Benutzer erstellt:

```text
Certificate Name:  vpn.admin-cert
Certificate Type:  User Certificate
CA:                grclab-CA
Key Length:        2048 bits
Common Name:       vpn.admin
```

---

## Firewall Rules / Firewall-Regeln

Two firewall rules were required:

Zwei Firewall-Regeln waren erforderlich:

### WAN Rule - Allow VPN Port / WAN-Regel - VPN-Port erlauben

```text
Action:     Pass
Interface:  WAN
Protocol:   UDP
Source:     any
Destination: WAN address
Port:       1194
Description: Allow OpenVPN traffic
```

### OpenVPN Interface Rule - Allow traffic through tunnel

```text
Action:     Pass
Interface:  OpenVPN
Protocol:   any
Source:     OpenVPN subnet (10.8.0.0/24)
Destination: any
Description: Allow VPN clients access to internal network
```

---

## Connection Test / Verbindungstest

### Validate tunnel IP / Tunnel-IP prÃ¼fen

```cmd
ipconfig
```

Expected result / Erwartetes Ergebnis:

```text
Ethernet adapter OpenVPN:
   IPv4 Address: 10.8.0.2
```

### Ping internal server / Internes System anpingen

```cmd
ping 192.168.56.26
```

Expected result / Erwartetes Ergebnis:

```text
Reply from 192.168.56.26: bytes=32 time=2ms TTL=127
```

---

## Validation Summary / ValidierungsÃ¼bersicht

| Test | Expected Result | Status |
|------|----------------|--------|
| CA and certificate created | Visible in Certificate Manager | Completed |
| OpenVPN server configured | Server appears in VPN list | Completed |
| VPN user created | User with certificate in User Manager | Completed |
| Firewall rules added | Rules on WAN and OpenVPN interfaces | Completed |
| Client config exported | .ovpn file generated | Completed |
| VPN connection established | Connected status in OpenVPN GUI | Completed |
| Tunnel IP assigned | 10.8.0.x address in ipconfig | Completed |
| Internal ping successful | Replies from 192.168.56.26 | Completed |

---

## Skills Demonstrated / Nachgewiesene Kompetenzen

* pfSense OpenVPN server configuration
* PKI and certificate management (CA, server cert, client cert)
* VPN tunnel design and implementation
* Firewall rule configuration for VPN traffic
* OpenVPN client installation and configuration
* Remote access security design
* Secure access validation

---

## Result / Ergebnis

A secure OpenVPN remote access solution was successfully configured on pfSense. Client certificates and user accounts were created, firewall rules configured, and the VPN connection validated end-to-end.

Eine sichere OpenVPN-FernzugangslÃ¶sung wurde erfolgreich auf pfSense konfiguriert. Client-Zertifikate und Benutzerkonten wurden erstellt, Firewall-Regeln konfiguriert und die VPN-Verbindung vollstÃ¤ndig validiert.
