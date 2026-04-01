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

<img width="576" height="460" alt="image" src="https://github.com/user-attachments/assets/f90cde6a-afe9-4674-a75c-7a36b909e0a9" />


---

## 2. Static IP Configuration

The server was initially assigned a DHCP address and then configured with a static IP.

Netplan configuration file: /etc/netplan/50-cloud-init.yaml

Applied configuration: sudo netplan apply

<img width="575" height="237" alt="image" src="https://github.com/user-attachments/assets/fa70fffd-d1b1-4fdc-ad08-94d1b5a5caa9" /> 

<img width="578" height="177" alt="image" src="https://github.com/user-attachments/assets/456be388-8ec0-49f1-80e8-77ea2ec04797" />

Verification: ip a


---

## 3. Web Stack Installation

Installed required packages for hosting osTicket: sudo apt install apache2 mariadb-server php libapache2-mod-php php-mysql unzip -y

Verified Apache service: systemctl status apache2

<img width="577" height="210" alt="image" src="https://github.com/user-attachments/assets/a94d8b83-6a9b-40ee-9996-e393e028ffc0" />

Accessed in browser: http://192.168.0.50

<img width="595" height="480" alt="image" src="https://github.com/user-attachments/assets/3dc98029-38ec-403c-a727-99e78e5e78af" />


---

## 4. PHP Extensions Installation

Installed required PHP modules: sudo apt install php-gd php-imap php-xml php-mbstring php-intl php-apcu -y

Restarted Apache: sudo systemctl restart apache2

<img width="582" height="471" alt="image" src="https://github.com/user-attachments/assets/62eb9e7f-e600-48c7-a745-33870a01af62" />


---

## 5. Database Configuration

Accessed MariaDB:sudo mysql

Executed:

CREATE DATABASE osticket;

CREATE USER 'osticketuser'@'localhost' IDENTIFIED BY 'password';

GRANT ALL PRIVILEGES ON osticket.* TO 'osticketuser'@'localhost';

FLUSH PRIVILEGES;

EXIT;


---

## 6. osTicket Installation

Downloaded and extracted osTicket:unzip osTicket-v1.18.zip


Moved files to web directory and set permissions: sudo chown -R www-data /var/www/html/osticket


Created configuration file: sudo cp /var/www/html/osticket/include/ost-sampleconfig.php /var/www/html/osticket/include/ost-config.php
sudo chmod 0666 /var/www/html/osticket/include/ost-config.php

Accessed installer: http://192.168.0.50/osticket

<img width="574" height="334" alt="image" src="https://github.com/user-attachments/assets/bbe6d1a3-28a4-4d35-bca7-4ac3edb6cee8" />


---

## 7. Post-Installation Hardening

Secured configuration file: sudo chmod 0644 /var/www/html/osticket/include/ost-config.php

Removed setup directory: sudo rm -rf /var/www/html/osticket/setup

<img width="586" height="63" alt="image" src="https://github.com/user-attachments/assets/d3872365-7599-4ea9-b3e0-44838a062eff" />


---

## 8. LDAP Integration

Downloaded LDAP plugin: cd /tmp
curl -L https://github.com/osTicket/osTicket-plugins/archive/refs/heads/develop.zip
 -o plugins.zip
unzip plugins.zip




