# osTicket-Help-Desk-Deployment-with-Active-Directory-Authentication

This project documents the deployment of a web-based help desk platform using osTicket on a Linux server, along with integration into an Active Directory environment using LDAP.

The goal was to simulate a realistic support environment where technicians can authenticate using domain credentials while managing tickets through a centralized system.

---
## Overview

An Ubuntu server (INFRA01) was configured to host osTicket using a standard LAMP stack:

- Apache (web server)
- MariaDB (database)
- PHP (application runtime)

After deployment, LDAP authentication was integrated so that user logins are validated against Active Directory instead of local application accounts.

---

## Key Components

- Ubuntu Server 24.04 LTS  
- Apache2  
- MariaDB  
- PHP + required extensions  
- osTicket  
- Active Directory (Domain Controller)  
- LDAP Authentication Plugin  

---

## Architecture

User Browser  
→ Apache Web Server  
→ PHP Application (osTicket)  
→ LDAP Plugin  
→ Active Directory (DC01)

## Screenshots

### osTicket Dashboard
![osTicket Dashboard]  (screenshots/dashboard.png)

### Login Page
![Login Page](screenshots/login.png)

### Apache Web Server Test
![Apache Default Page](screenshots/apache.png)

---

## Deployment Summary

### 1. Server Setup
- Installed Ubuntu Server in Proxmox
- Configured static IP (192.168.0.50)
- Set DNS to domain controller (192.168.0.10)

### 2. Web Stack Installation
Installed required packages: sudo apt install apache2 mariadb-server php libapache2-mod-php php-mysql unzip -y

Verified Apache was running and accessible from a browser.

---

### 3. osTicket Installation
- Deployed osTicket to `/var/www/html`  
- Configured database connection  
- Created administrative account  
- Completed installer successfully  

Post-install steps:
- Restricted config file permissions  
- Removed setup directory  

---

### 4. Active Directory Integration (LDAP)
- Installed LDAP authentication plugin  
- Configured connection to domain controller  

Key settings:
- Domain: lab.local  
- LDAP Server: 192.168.0.10  
- Search Base: DC=lab,DC=local  

DNS was required to function correctly for LDAP authentication.

---

## Authentication Flow

User Login  
→ osTicket Application  
→ LDAP Plugin  
→ Active Directory  
→ Access Granted / Denied  

---

## Issues Encountered

### DNS Resolution Failure
Initial DNS queries failed, which prevented LDAP authentication from working.

**Resolution:**  
Configured the server to use the domain controller (192.168.0.10) as its primary DNS server.

---

### LDAP Dependency Errors
The LDAP plugin initially failed due to missing dependencies.

**Resolution:**  
Installed required PHP modules and verified correct plugin placement in the osTicket directory.

---

## Result

The system is fully operational and supports:

- Ticket creation and tracking  
- Administrative ticket management  
- Role-based access control  
- Authentication through Active Directory  

This setup reflects a basic enterprise help desk environment where authentication is centralized and services are internally hosted.

---

## Notes

This project focuses on system deployment, service integration, and troubleshooting within a domain-based environment. It is designed to demonstrate practical understanding of how help desk platforms integrate with directory services.

---

## License

This project is licensed under the MIT License.
