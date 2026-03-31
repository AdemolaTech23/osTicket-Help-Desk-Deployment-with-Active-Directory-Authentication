# osTicket Deployment and Active Directory Integration

## Overview

This document outlines the deployment of osTicket on an Ubuntu server and its integration with Active Directory using LDAP authentication.

The system was configured to simulate a centralized help desk environment with domain-based authentication.

---

## System Information

- Hostname: infra01  
- OS: Ubuntu 24.04.4 LTS  
- IP Address: 192.168.0.50  
- Domain Controller: 192.168.0.10  
- Domain: lab.local  

---

## 1. Initial Server Setup

After installing Ubuntu Server in Proxmox, the system was verified and accessed using the local administrative account.

Basic tools were installed for system administration: sudo apt install net-tools curl git nmap tcpdump -y


