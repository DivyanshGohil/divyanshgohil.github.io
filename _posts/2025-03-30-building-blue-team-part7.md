---
title: 'Building Blue Team Home Lab - Part 7 : Corporate LAN (End Devices)'
date: 2025-03-30
permalink: /posts/2025/03/building-blue-team-part7/
tags:
  - Blue Team
  - Home Lab
---

###  Introduction
After a while, I returned with a new tutorial, a continuation of my **Blue Team Home Lab** series, and this time it’s about adding the end devices to our lab. For this part, we are going to use **Windows 7** and **Windows 10** evaluation images, which can be downloaded from [here](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/). Download the **IE11 on Win7** and **MSEdge on Win10** images.

---

### Prerequisite

Before we continue, make sure you’ve completed all the steps from **Part 6** where we set up the **Domain Controller (DC)**. In this part, we'll join VMs to the domain.

Also, ensure both the **firewall** and **DC** are powered on.

---

### Windows 7 VM

Let’s start with the old one. Yes, I know **Windows 7** is not officially supported anymore, but it's still widely found in many environments.

### VM Configuration

- **Name**: Windows 7 Host
- **Memory**: 4GB  
- **Processors**: 1 CPU  
- **HDD**: 40GB  
- **Network Adapter**: vmnet20  

> The installation of Windows 7 is not covered here—check YouTube for guides.

### Post-Installation Configuration

#### Enable ICMP in Windows Firewall

1. Open `Control Panel > System and Security > Windows Firewall`
2. Click `Advanced settings`
3. Enable the following rule for **Private, Public, and Domain** profiles:
   - **File and Printer Sharing (Echo Request - ICMPv4-In)**

#### Rename the Computer

1. Go to `Control Panel > System and Security > System`
2. Click `Change settings`
3. Set a **Computer description**, e.g., `Meeting Room PC01`
4. Click `Change`, and set **Computer name** to: `RC-MEETING-PC01`
5. Save and **restart** the VM

### Joining the Domain

1. Return to `System Properties > Change`
2. Choose **Domain** instead of workgroup
3. Enter your **domain name**
4. When prompted, provide **Administrator credentials**
5. Restart the VM upon success

### Testing Domain User

1. On login screen, click `Switch user > Other User`
2. Log in with the **HR** user from the previous article
3. Open `\\CHDC01\cyberhubshared\HR` in File Explorer to test access
4. From the DC, run: `ping RC-MEETING-PC01` to test connectivity

---

### Windows 10 VM

Now let’s set up the **Windows 10** machine.

### Enable ICMP in Firewall

1. Go to `Control Panel > System and Security > Windows Defender Firewall`
2. Click `Advanced settings`
3. Enable **File and Printer Sharing (Echo Request - ICMPv4-In)** for all profiles

### Rename the Computer

1. Go to `System > Change settings`
2. Set a **Computer description** and **Computer name** to reflect a corporate device
3. Save and **restart** the VM

### Joining the Domain

1. Go back to `System Properties > Change`
2. Enter the **domain name**
3. Provide **Administrator credentials**
4. Restart the VM if joined successfully

### Testing Domain User

1. On login screen, click `Other User`
2. Log in using the **IT user** from the previous article
3. Access: `\\CHDC01\cyberhubshared\IT OPS`
4. Create a test file if needed
5. From the DC, ping the Windows 10 machine to confirm connectivity

---

### Summary

We now have two end devices added to our lab that simulate corporate machines:

- **Windows 7**: RC-MEETING-PC01
- **Windows 10**: [Your chosen name]

Both are domain-joined and have access to shared company resources. These machines now present new attack surfaces and monitoring opportunities for Blue Team exercises.

---

**Next Up**: We’ll deploy a **Linux server** that acts as a simple **web and database server**, complete with **exploitable vulnerabilities** for future simulation and defense scenarios.

Stay tuned!
