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

---

## Deployment Summary

### 1. Server Setup
- Installed Ubuntu Server in Proxmox
- Configured static IP (192.168.0.50)
- Set DNS to domain controller (192.168.0.10)

### 2. Web Stack Installation
Installed required packages:

