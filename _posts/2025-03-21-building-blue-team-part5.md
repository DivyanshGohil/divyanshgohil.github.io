---
title: 'Building Blue Team Home Lab - Part 5 : Malware Analysis'
date: 2025-03-21
permalink: /posts/2025/03/building-blue-team-part5/
tags:
  - Blue Team
  - Home Lab
---


###  Introduction

In the previous part, we built a DFIR environment. Now, it's time to build a secure **malware analysis environment**.  
⚠️ *Malware analysis is risky. Only proceed if you understand how to sandbox and isolate systems properly.*

---

### 🌐 Networking for Malware Analysis

A **sandboxed network** is critical. Use an isolated VLAN (e.g., `VLAN 99`) where malware can’t escape to other VMs or your host.

### 🧰 Safe Networking Options

1. **Firewall Isolation**  
   - Block incoming/outgoing traffic on DFIR VM.
   - Use snapshots before enabling Internet to download malware samples.

2. **Dual VLAN Approach**  
   - Use VLAN 50 to download samples, then switch to VLAN 99 for analysis.

3. **Preferred Method**  
   - Download samples on the DFIR VM, transfer using **SCP** or **shared folders** to malware analysis VMs on VLAN 99.

---

## 🪟 Windows Malware Analysis VM

### Tools:
- **Microsoft Edge on Windows 10** VM
- **[Flare VM](https://github.com/mandiant/flare-vm)** – Windows security distribution with analysis tools

### Setup Instructions:
1. Import Windows 10 VM
2. Expand disk to **80GB**, configure network as **NAT**
3. Activate Windows license (valid for 90 days)
4. Disable:
   - Windows Defender
   - Windows Firewall
   - Windows Updates
5. Create a snapshot (“Vanilla”)

### Install Flare VM:
1. Run below powershell command as Administrator. You will be prompt with the question to confirm the changes. Press the Y button and then press Enter.
```powershell
Set-ExecutionPolicy Unrestricted
.\install.ps1
```
2. Provide password for IEUser.
3. Installation may take a few hours.

### Post-Installation:
1. Change network to VLAN 99, assign static IP.
   
| Parameter   | Value           |
|-------------|-----------------|
| **IP Address**   | 10.0.99.22   |
| **Subnet Mask**  | 255.255.255.0   |
| **Gateway**      | 10.0.99.254     |
| **DNS Server**   | 10.0.99.254         |

2. Enable SSH and install WinSCP for file transfers


## 🐧 Linux Malware Analysis VM (REMnux)

### Tools:
- **REMnux** – Linux distro for reverse-engineering and malware analysis

### Setup Instructions:
1. Download REMnux VM and import into your virtualization software.

2. Set network to **NAT**, then update the system:
```bash
sudo apt update && sudo apt upgrade -y
```
3. Configure static IP in VLAN 99. Edit the netplan configuration file (e.g., `/etc/netplan/01-netcfg.yaml`):
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      dhcp4: no
      addresses: [10.0.99.22/24]
      gateway4: 10.0.99.254
      nameservers:
          addresses: [10.0.99.254]
          search: [cyber.hub]
```

4. Save the file and execute the command ```sudo netplan apply``` to apply network changes. Then verify changes.


---

💾 **Create a new snapshot** so you can always revert to it when starting with a new analysis.

---
## 🎓 Recommended Tutorials

- **[Malware Analysis Bootcamp](https://www.youtube.com/playlist?list=PLBf0hzazHTGOEuhPQSnq-EjCzjWZ_TIFc)** – HackerSploit's guide with Flare VM  
- **[Noob2Ninja Malware Analysis Course](https://www.youtube.com/playlist?list=PL_Ubt4He1EFlS5Z4C3OXN3dlbGf2e8K0X)** – By Neil Fox, builds a lab from scratch with Windows 7

---

## ✅ Summary

You've now set up isolated Windows and Linux malware analysis environments using **Flare VM** and **REMnux**.  
🧠 Always be cautious—malware can escape VMs and affect host machines.

---
