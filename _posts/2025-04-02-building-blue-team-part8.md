---
title: 'Building a Blue Team Home Lab - Part 8 : Web Server'
date: 2025-04-02
permalink: /posts/2025/03/building-blue-team-part8/
tags:
  - Blue Team
  - Home Lab
---


###  Introduction

Hello everyone! I know it’s been a while—life got a bit hectic, and I needed a break from the lab and the website. But I’m back, and it’s time to move forward with something exciting: setting up a **vulnerable web server**.

We’ll deploy **Ubuntu Server 22.04 LTS** and install **DVWA (Damn Vulnerable Web Application)**. This setup will be super useful for simulating web attacks, analyzing logs, and practicing Blue Team detection techniques.

---

## 🖥️ Ubuntu Installation & Setup

I won’t walk you through installing Ubuntu Server—there are plenty of guides out there. Here’s [one I used on YouTube](https://www.youtube.com) (yep, first result I clicked 😅).

> ⚠️ Use **NAT or Bridged network adapter** during install for updates and downloads.

### 🛠️ Install Required Packages

```bash
apt update
apt install -y apache2 mariadb-server mariadb-client php php-mysqli php-gd libapache2-mod-php nano unzip fping
```

## 📦 Download DVWA
```
cd /var/www/html
wget https://github.com/digininja/DVWA/archive/master.zip
unzip master.zip
mv DVWA-master DVWA
```

## 🌐 Set Static IP (VLAN 20)
Edit /etc/netplan/01-network-config-01.yaml
```
network:
    version: 2
    renderer: networkd
    ethernets:
        ens33:
            addresses:
                - 10.0.20.10
            nameservers:
                addresses: [10.0.20.254]
            routes:
                - to: default
                  via: 10.0.20.254

```
>🧠 Use ip a to confirm your interface name (mine is ens33).
Apply the changes:
```
  netplan apply

```
## 🧩 DVWA Installation & Configuration
Start Apache:
```
systemctl start apache2
```
>Access in Browser:
>Visit http://10.0.20.10/DVWA/ from your host machine.

## 🗃️ Database Setup
Go to the DVWA interface → Setup / Reset DB → Click Create / Reset Database.

To make the DB more insecure (for testing, of course 😈), allow remote access:

Edit /etc/mysql/mariadb.conf.d/50-client.cnf:
```
#bind-address = 127.0.0.1
bind-address = 0.0.0.0
```
Then:
```
systemctl restart mariadb
ss -tnlp
```
> ✅ Ensure DB is accessible from any source.

## 🔐 Fix Permissions & PHP Settings

```
chmod 777 /var/www/html/DVWA/hackable/uploads/
chmod 777 /var/www/html/DVWA/external/phpids/0.6/lib/IDS/tmp/phpids_log.txt
chmod 777 /var/www/html/DVWA/config
```
Edit your PHP config and make sure:

```
allow_url_fopen = On
allow_url_include = On
```

## 🌐 Apache & DNS Setup
Configure Virtual Host
```
cd /etc/apache2/sites-available
cp 000-default.conf system.cyber.hub.conf
nano system.cyber.hub.conf
```
Paste:

```
<VirtualHost *:80>
        ServerName system.cyber.hub

        ServerAdmin cyber@hub
        DocumentRoot /var/www/html/DVWA

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Enable it:
```
a2ensite system.cyber.hub.conf
a2dissite 000-default.conf
systemctl restart apache2
```

Edit Local DNS
Edit /etc/hosts on the Linux server:
```
127.0.0.1 localhost system.cyber.hub
```
Edit /etc/hosts on your host machine:
```
10.0.1.50 firewall.cyber.hub
10.0.20.10 system.cyber.hub
```
Now you can access DVWA via http://system.cyber.hub.

## 📡 Active Directory Configuration
For other VMs in your domain to access the web server, create an A record for system.cyber.hub just like you did for the firewall in Part 6.

Try accessing the web app from your Windows 7 VM to confirm everything is working.

💾 Don’t forget to take snapshots of both your Linux web server and Active Directory VMs.

## ✅ Summary
And there you have it—a fully working web server running DVWA, tied into our Blue Team lab. This box is now your go-to for testing:

Web attacks (SQLi, XSS, etc.)

Logging and alerting

Access control analysis

Next up, we’ll add Kali Linux as our external attacker box and later move into SIEM integration to start monitoring all this juicy traffic. 😎

Until next time—stay sharp and keep building!
