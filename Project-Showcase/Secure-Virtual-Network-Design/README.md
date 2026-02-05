# 🛡️ Secure Virtual Network Design & Implementation
**Project Type:** System Administration & Network Security  
**Authors:** Mounim Nadir & Mohamed Ait Ezzaouite  
**Context:** MST SITBD - Module: Administration Système et Réseaux  

## 📌 Executive Summary
This project demonstrates the design and secure deployment of a segmented enterprise network using **pfSense** and **Linux (Ubuntu)**. The infrastructure is divided into strict security zones (WAN, LAN, DMZ) to ensure isolation of critical assets while maintaining service availability.

The final architecture was audited using **Wireshark** to validate traffic flow and rule enforcement.

## 🏗️ Technical Architecture
### 1. Network Topology (Segmentation)
The network is segmented into three isolated zones to prevent lateral movement in case of a breach:
* **WAN (Untrusted):** External internet connection (em0).
* **LAN (Trusted):** `192.168.10.0/24` - Dedicated to internal users (Students/Admin). Secured by a **Captive Portal**.
* **DMZ (Semi-Trusted):** `192.168.11.0/24` - Hosts the public-facing Web Server (`www.uthmandevsec.sn`).
    * *Security Rule:* The DMZ is strictly blocked from initiating connections to the LAN.

### 2. Services Deployed
* **Firewall & Routing:** pfSense 2.6.0 (Stateful inspection, NAT, DHCP).
* **DNS Infrastructure:** Hybrid setup using **Unbound DNS Resolver** (pfSense) and **Bind9** (Ubuntu) for internal name resolution.
* **Web Server:** Apache2 hosting the "Gotto Job Portal" application.
* **Identity Management:** Local user database integrated with a Captive Portal for network access control.

## 🔍 Security Validation (Proof of Work)
We utilized **Wireshark** to audit the security policies:
1.  **DNS Leak Test:** Confirmed that internal DNS queries (`nslookup`) are handled locally by the firewall (192.168.10.1) without leaking to public resolvers.
2.  **Traffic Analysis:** Validated that HTTP traffic (Port 80) is permitted from LAN to DMZ, while ICMP traffic from DMZ to LAN is dropped (Default Deny).

## 📂 Project Resources
* **[📄 Full Technical Report (PDF)](./Rapport_Securisation_Reseau_Virtuel.pdf)**: Detailed step-by-step configuration guide, including screenshots of pfSense rules and VirtualBox network settings.
