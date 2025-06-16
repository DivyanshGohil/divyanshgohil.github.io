---
title: 'Building Blue Team Home Lab - Part 6 : Corporate LAN (Domain Controller)'
date: 2025-03-25
permalink: /posts/2025/03/building-blue-team-part6/
tags:
  - Blue Team
  - Home Lab
---

###  Introduction

Welcome back to the lab series! It’s been a while. But now we're diving into setting up a **corporate network** with **Windows Server 2019** as our Domain Controller (AD, DNS, File Share Server).

> ⚠️ **Note:** Microsoft provides 180-day evaluation versions of Windows Server. These are **not for production or personal device use**.

---

### 🧱 Installation Steps (Quick)

1. Download the ISO from Microsoft’s website.
2. Create a new VM (Name it: `Windows Server 2019`).
3. Install with default options (set your own password).
4. Once installed, take a **vanilla snapshot** for easy revert.

---

## 🔧 Configuration


### 🖧 Network & Hostname Setup
```bash
IP Address:      10.0.20.5  
Subnet Mask:     255.255.255.0  
Default Gateway: 10.0.20.254  
DNS:             10.0.20.254  
Hostname:        CHC01
 ```

### 🖥️ Change Hostname

Change the hostname in **System Properties**, e.g., `CHC01`, and restart the VM.

---

### 📦 Roles & Features

1. Open **Server Manager** > **Manage** > **Add Roles and Features**  
2. Select and install the following:
   - Active Directory Domain Services  
   - DHCP Server  
   - DNS Server  
   - File and Storage Services  
   - Remote Access  
3. After installation, click **"Promote this server to a domain controller"**
4. Create a **new forest**, set domain name, and **Administrator password**
5. Reboot and log in using: Administrator@yourdomain

---

### 📡 DHCP Configuration

1. Open **DHCP**: Server Manager > Tools > DHCP  
2. Right-click **IPv4** > **New Scope**
3. Use the following settings:  
- **Name**: `corp_lan`  
- **Range**:  
  ```
  Start IP: 10.0.20.51  
  End IP:   10.0.20.151  
  Subnet:   255.255.255.0 (/24)
  ```  
- **Set Domain Controller (10.0.20.5) as**:
  - Default Gateway  
  - DNS Server  
  - WINS Server  

---

### 🧭 DNS Configuration

1. Open **DNS** via Server Manager > Tools > DNS  
2. Create **Reverse Lookup Zone**  
    - Network ID: `10.0.20`
3. Add an **A Record** for firewall:
   - Hostname: firewall
   - IP: 10.0.20.254
4. Verify using:
```bash
nslookup 10.0.20.254
```
---

### 🛡️ Routing
1. Open Routing and Remote Access
2. Configure Routing
    - Choose Custom > Enable LAN Routing
3. Add Static Route:
    - Destination: 10.0.50.55  
    - Netmask: 255.255.255.255  
    - Gateway: 10.0.20.254

---

### 🔓 Disable Password Complexity  
Follow this guide to disable password complexity (for testing weak password scenarios):  
[Disable Password Complexity on Server 2016](https://www.wintips.org/how-to-disable-password-complexity-requirements-on-server-2016/)

---

### 👤 Create Users
- Open **Active Directory Users and Computers**  
- Right-click **Users** > **New > User**  
- Naming format: `firstname.lastname`  
- Use a mix of:
  - ✅ Strong passwords  
  - ❌ Weak passwords from `rockyou.txt`  
- Set password to **never expire**

---

### 🧑‍🤝‍🧑 Create Groups 
- Create new **OU** (Organization Unit): `Groups`  
- Inside, create groups:
  - `HR`
  - `Marketing`
  - `IT OPS`
- Assign users to appropriate groups
- Add a few users to the **Administrators** group


### 🛡️ Configure Local Admin GPO  
- Open **Group Policy Management**  
- Create a new GPO: `Local Admin GPO`  
- Edit GPO: `Computer Configuration > Policies > Windows Settings > Security Settings > Restricted Groups`
- Add Group: `Local Adminstrator - Workstations`
- Add users/groups who should have local admin rights

---

### 📁 Shared Folder (SMBv1)
#### ⚠️ Why SMBv1?

We're enabling **SMBv1** to simulate insecure configurations for Blue Team detection and mitigation practice.  
**Note:** SMBv1 is deprecated and insecure — avoid using it in production environments.

---

### 📂 Folder Structure

Create the following structure on the `C:` drive:
```
C:\
└── racoonshared
    ├── HR
    ├── IT OPS
    └── Marketing
```

---

### 🔧 Sharing & Permissions

For **each** folder inside `cyberhubshared` (including the parent):

1. Right-click the folder → **Properties**
2. Go to the **Sharing** tab
3. Click **Share**
4. Add the **corresponding group** (e.g., HR group for HR folder)
5. Set **Permission Level** to **Read/Write**
6. Click **Share** to apply

Repeat for:
- `IT OPS` → IT OPS group  
- `Marketing` → Marketing group  
- `cyberhubshared` (optional: shared with all or admin group)

---

### 📝 Add Sample Files

To simulate realistic conditions, add:
- A few **text files**
- Some **images or PDFs**
- Files with **fake sensitive names** like `employee_data.txt` or `Q3_budget.xlsx`

✅ Now your SMBv1 shares are live and ready for vulnerability scanning, detection, and defense testing.

---

### ✅ Summary  
Congrats! You now have a basic **Corporate LAN** setup with:

- ✅ Active Directory  
- ✅ DHCP & DNS  
- ✅ Static Routing  
- ✅ Shared SMBv1 folders  
- ✅ Weak password policy for attack simulation  

