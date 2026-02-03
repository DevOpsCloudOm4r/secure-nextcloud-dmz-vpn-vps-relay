# secure-nextcloud-dmz-vpn-vps_relay
Secure Nextcloud Architecture implemented as part of the IHK final project (Fachinformatiker Systemintegration).
![Netzwerk Architektur](netzwerk-diagramm.svg)

# Secure Nextcloud Architecture – DMZ & VPN Relay Design

Production-ready Nextcloud deployment using Proxmox, OPNsense and WireGuard.
External access is provided via a VPS relay – no port forwarding required.

## Project Overview
This repository documents the design and implementation of a secure, self-hosted Nextcloud platform
operated within a segmented network architecture.

The project was implemented as part of the official **IHK final project (Fachinformatiker Systemintegration)**  
and follows real-world enterprise security principles.

A key constraint of the environment was that **no inbound port forwarding** was permitted on the school
network. To solve this limitation, external access was implemented using a **VPS-based WireGuard VPN relay**,
ensuring that no internal services are directly exposed to the internet.

---

## Architecture Summary
- **Virtualization Platform:** Proxmox VE  
- **Security Gateway:** OPNsense Firewall  
- **Network Segmentation:**  
  - LAN (172.16.201.0/24)  
  - DMZ (10.10.10.0/24)  
  - VPN Tunnel Network  
- **Service:** Nextcloud (HTTPS, hardened)  
- **External Access:** VPS + WireGuard VPN  
---
## 📄 Documentation
- [IHK Project Documentation (PDF)](docs/IHK-Projektdokumentation.pdf)

---

## Access Paths

### Internal Access (School Network)

# Client → OPNsense → DMZ → Nextcloud

- HTTPS (443) only  
- Controlled firewall rules  
- No DMZ-to-LAN communication allowed  

### External Access (Remote Users)

# Client → Internet → VPS → WireGuard → OPNsense → DMZ → Nextcloud

- No port forwarding on the school router  
- Encrypted VPN tunnel (WireGuard)  
- Access limited strictly to Nextcloud HTTPS  

---

## Security Design Principles
- Strict network segmentation (LAN / DMZ / VPN)
- Central security enforcement via OPNsense
- Key-based VPN authentication (WireGuard)
- HTTPS encryption using an internal Certificate Authority
- Two-Factor Authentication (administrative accounts)
- Fail2Ban for brute-force protection
- Hardened file permissions and security headers
- Explicit blocking of lateral movement (DMZ → LAN, VPN → LAN)

---

## Why a VPS-Based VPN Relay?
- School infrastructure does not allow inbound connections
- No exposure of internal services to the public internet
- Clear separation between external and internal trust zones
- Centralized access control and auditability
- Realistic solution for restricted enterprise environments

---

## Technologies Used
- Proxmox VE
- OPNsense Firewall
- WireGuard VPN
- Nextcloud
- Debian / Linux
- OpenSSL (internal CA)
- diagrams.net (draw.io)

---

## Project Context
This project was developed as part of the **IHK final examination** and demonstrates
practical system integration skills, including secure network design, firewalling,
VPN implementation, and service hardening.

The architecture is designed to be modular and extensible for future enhancements
such as monitoring, backups, or additional DMZ services.



