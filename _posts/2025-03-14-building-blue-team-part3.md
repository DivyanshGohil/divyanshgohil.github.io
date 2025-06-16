---
title: 'Building Blue Team Home Lab - Part 3 : Deploying a Firewall'
date: 2025-03-14
permalink: /posts/2025/03/building-blue-team-part3/
tags:
  - Blue Team
  - Home Lab
---



## 🛡️ Building Blue Team Home Lab - Part 3 : Deploying a Firewall  


---

### 🔧 Changes to be Done in Previous Setup  
1 - Corrected Outbound rules; interface for source `10.0.20.0/24` should be `CORPORATE_LAN_VLAN20`.  
2 - Disabled DHCP service; domain controller now provides DHCP.  
3 - Added VLAN 99 for malware analysis.


---


## 🔥 Firewall: pfSense  

We’ll use **pfSense** – an open source, powerful firewall suitable for both lab and production use.

### 💻 VM Specifications  
- **CPU:** 1  
- **RAM:** 512MB  
- **HDD:** 30GB  
- **NICs:** 6  
  - Bridged  
  - vmnet1 (Management)  
  - vmnet10 (Corporate WAN)  
  - vmnet20 (Corporate LAN)  
  - vmnet50 (Security)  
  - vmnet99 (Isolation)  

> 💡 **Why 6 NICs?**  
One per VLAN, plus one bridged interface to provide outbound traffic for Security VLAN.

---

## 🧱 Installation  

Install pfSense using default settings. Once booted:  
1. Configure WAN & Management interfaces (CLI).  
2. Use the table below for IP assignment:

| Interface        | IP Address        |
|------------------|------------------|
| WAN              | 192.168.1.50/24  |
| Management       | 10.0.1.50/24     |
| Corporate WAN    | 10.0.10.254/24   |
| Corporate LAN    | 10.0.20.254/24   |
| Security         | 10.0.50.254/24   |
| Isolation LAN    | 10.0.99.254/24   |

> ⚠️ WAN subnet depends on your actual ISP network (commonly 192.168.1.0/24 or 192.168.0.0/24).

---

## ⚙️ Configuration  

### 🌐 Interfaces  
1. Navigate to `Interfaces > Interface Assignments`  
2. Add all NICs, save.  
3. Enable and set for each:  
   - **Description:** `$NETWORK_NAME_VLAN<VLAN_ID>`  
   - **Static IP** from table above (/24)  
   - **Only WAN** should have Upstream Gateway, Block Private & Bogon networks.

---

### 🛠️ Basic Setup  
Go to `System > General Setup`  
- **Hostname:** firewall  
- **Domain:** cyber.hub  
- **DNS Servers:** 9.9.9.9, 1.1.1.1 *(or 8.8.8.8, 8.8.4.4)*  
- **Timezone:** Etc/UTC  
- **Theme:** Your preference  

Then, in `System > Advanced > Admin Access`:  
- **Protocol:** HTTPS  
- **Enable Secure Shell**

---

## 🔒 Firewall Rules  

> Start with allowing all traffic, then gradually restrict based on your lab requirements.

### 🌐 WAN (`192.168.1.50/24`)  
- ⛔ Block Private & Bogon networks (default)  
- ⛔ No inbound from internal VLANs unless explicitly required

### 🧑‍💻 MANAGEMENT (`10.0.1.50/24`)  
- ✅ Access from local machine (vmnet1)  
- ✅ Anti-lockout rule (default)  
- ⛔ Disable default IPv6 pass rule  
- ⛔ No access from other VLANs (Security, Isolation, etc.)

### 🖧 CORPORATE WAN (`10.0.10.254/24`)  
- ✅ Allow from Corporate LAN (`10.0.20.0/24`)  
- ✅ Outbound access to fake WAN or internet  
- ⛔ Deny from Security and Isolation VLANs

### 🖧 CORPORATE LAN (`10.0.20.254/24`)  
- ✅ Allow to Corporate WAN (`10.0.10.0/24`)  
- ✅ Allow to Management (`10.0.1.0/24`)  
- ⛔ Deny to WAN and Security by default  
- ⛔ Block traffic to Isolation VLAN
  
### 🛡️ SECURITY (`10.0.50.254/24`)  
- ✅ Allow to Corporate LAN (`10.0.20.0/24`)  
- ✅ Allow to Isolation VLAN (`10.0.99.0/24`)  
- ⛔ Deny to WAN, Management, Corporate WAN  
- ⛔ Block all unnecessary outbound unless via VPN

### 🔬 ISOLATION (`10.0.99.254/24`)  
- ⛔ Deny to all other VLANs  
- ✅ Optional: Allow only logging or update servers  
- ✅ Add explicit deny rule for extra safety

---

### 📤 Outbound NAT Rules  

Set NAT rules at `Firewall > NAT > Outbound`:

| Source VLAN           | Destination        | NAT Interface              |
|-----------------------|--------------------|----------------------------|
| `10.0.50.0/24`        | Internet           | WAN                        |
| `10.0.20.0/24`        | 10.0.10.254 (Fake) | CORPORATE_LAN_VLAN20       |
| `10.0.99.0/24`        | ✖️ (No Internet)    | N/A (Blocked)              |

> ⚠️ Double-check interface bindings in the Outbound NAT tab—make sure, for example, `CORPORATE_LAN_VLAN20` is used correctly instead of defaulting to WAN.

---


## 📌 Summary  

We've deployed a pfSense firewall, created VLAN rules, assigned IPs, and set up access. With traffic control in place, we're ready to move on to **building our security environment** in the next part. Stay tuned! 🚀

---
**🔗 [Reference](https://facyber.me/posts/blue-team-lab-guide-part-3/)**  
