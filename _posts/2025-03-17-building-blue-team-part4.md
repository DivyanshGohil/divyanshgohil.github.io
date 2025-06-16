---
title: 'Building Blue Team Home Lab - Part 4 : DFIR'
date: 2025-03-17
permalink: /posts/2025/03/building-blue-team-part4/
tags:
  - Blue Team
  - Home Lab
---

###  Introduction
Welcome to **Part 4** of the Blue Team Home Lab series! In this section, we’ll be setting up a **DFIR (Digital Forensics and Incident Response)** VM using [**Tsurugi Linux**](https://tsurugi-linux.org/) a feature-rich and powerful distro designed for digital forensics.

> **Note:** This guide focuses on environment setup. You are encouraged to explore the tools and techniques yourself.

---

### What We’ve Done So Far

In [Part 3](https://divyanshgohil.github.io/2025/03/14/Building-Blue-Team-Home-Lab-Part-3.html), we deployed our first VM a **firewall**. We:
- Configured VLANs
- Set up DNS & DHCP
- Created basic firewall rules

Now, it’s time to **expand our security team** by introducing the **DFIR machine**, among others.

---

### Why Tsurugi?

While **SANS SIFT Workstation** is a popular choice, we’ve selected **Tsurugi Linux** for:
- Lightweight **MATE desktop environment**
- Unique toolset
- Aesthetic samurai vibes 

> Try both Tsurugi and SIFT. Use what feels right.

---

### Network Topology Overview

The **DFIR VM** will:
- Access the **internet** for updates, OSINT, downloads
- Access **Corporate LAN** for log collection
- Be isolated from general internal access (**one-way access**)

---

### Tsurugi Installation Steps

### 1. Download and Import OVA
- Get the OVA from the [official site](https://tsurugi-linux.org/)
- Import it into **VMWare** or **VirtualBox**

### 2. VM Settings
- CPU: 4 Cores (2 processors × 2 cores)
- Network Adapter: Assign to **VLAN 50** (e.g., `vmnet50`)

### 3. First Boot
- Username: `tsurugi`
- Password: `tsurugi`

> Enjoy the samurai-themed desktop!

---


### DFIR VM Setup Guide

This section covers **hostname configuration**, **network settings**, **tool installation**, and **browser enhancements** for your DFIR virtual machine.

---

### Hostname Setup

**Edit** `/etc/hosts`

```bash
127.0.0.1   localhost
10.0.50.44  dfir dfir.cyber.hub
```
**Static IP & Host Override**

> Go to: System > Preferences > Internet and Network > Advanced Network Configuration

**Configure the following:**

- **Static IP**
- **Gateway**
- **DNS**
- **Search domain**

> **Reboot your VM** after completing this configuration to apply changes.

---

### Firewall DNS Resolver Host Override (pfsense VM)

> Navigate to: Services > DNS Resolver > General Settings
Under **Host Overrides**, click **Add** and enter:

- **Host:** `dfir`
- **Domain:** `cyber.hub`
- **IP Address:** `10.0.50.44`

> Use the firewall’s **Diagnostics > Ping** tool to verify that the FQDN resolves correctly.

---

### Snapshot Reminder

**Create a VM snapshot now!**  
It will serve as your rollback point in case you break something or need to revert to a clean, functional state.

### Additional Web Tools

Now let’s add new bookmarks to my still favorite browser, **Firefox**:

- [VirusTotal](https://www.virustotal.com/)
- [Hybrid-Analysis](https://www.hybrid-analysis.com/)
- [Talos Intelligence](https://talosintelligence.com/)
- [urlscan.io](https://urlscan.io/)
- [Whois](https://who.is/)
- [MXToolbox](https://mxtoolbox.com/)
- [URL2PNG](https://www.url2png.com/)
- [OTX (AlienVault)](https://otx.alienvault.com/)
- [OUI Lookup](https://www.wireshark.org/tools/oui-lookup.html)
- [IP Location](https://www.iplocation.net/)
- [A-Packets](https://apackets.com/)
- [Wannbrowser](https://wannbrowser.com/)
- [de4js (JavaScript Unpacker)](https://lelinhtinh.github.io/de4js/)
- [Geolocate (Google Geolocation API)](https://developers.google.com/maps/documentation/geolocation/overview)
- [Yandex](https://www.yandex.com/)
- [Wayback Machine](https://web.archive.org/)
- [Fake Mail Generator](https://www.fakemailgenerator.com/)

---

### Summary

You now have a fully configured **DFIR Virtual Machine** ready for:

-  **OSINT**
-  **Incident Response**
-  **Log Analysis**
-  **General Forensics**

---

### Reference  
  *Published by Marko Andrejic*  
  - [https://facyber.me/posts/blue-team-lab-guide-part-4/](https://facyber.me/posts/blue-team-lab-guide-part-4/)

---

> **Disclaimer:**  
> This guide is intended for setting up a lab environment only.  
> It does **not** teach how to perform DFIR investigations or malware analysis.  
> Always use these tools and techniques **ethically** and within **legal boundaries**.

