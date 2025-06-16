---
title: 'Building a Blue Team Home Lab - Part 9 : Bandito'
date: 2025-04-04
permalink: /posts/2025/03/building-blue-team-part9/
tags:
  - Blue Team
  - Home Lab
---



# 🛡️ Building a Blue Team Home Lab - Part 9 : Bandito


---

## 👋 Introduction

We are close to the end of this guidance toward building the **Blue Team Home Lab**. Last time we configured a **web server** that hosts a website and a **MariaDB** database. I’ve made some changes in the previous article, so be sure to check them before continuing here.

This time, we will focus on creating a **Bandito network**—or better said, simulating an **external network** where our threats originate from. This network will contain a **Kali Linux** machine, which we’ll use to simulate attacks that we can later detect using our **SIEM**.

Let’s get started.

---

## 💾 Installation and Configuration

First, download the Kali Linux VM that suits your needs. In my case, I used the **VMware** version.

Once downloaded, import the VM into **VMware** or **VirtualBox** and leave the configuration settings as default. For now, use either **NAT** or **Bridged mode** for networking. Once done, power on the VM and log in.

Run system updates:

```bash
sudo apt update
sudo apt upgrade
```

>After all updates are installed, reboot the VM. Once rebooted, shut it down.

## 🌐 Network Configuration
Now let’s reconfigure our Bandito (Kali Linux) machine to use a Fake WAN network. This simulates Internet access without actually exposing the VM, helping prevent accidental outbound attacks into real environments.

In your VMware/VirtualBox settings, change the network adapter to VLAN 10 (or your designated external network).

Then power on the machine.

🧠 Tip: Create a snapshot of the VM at this point. It will serve as a clean backup in case anything breaks later.

## 🔥 Firewall Configuration
With the current setup, our Bandito machine is logically coming from an "external" network. In a real scenario, there would be firewalls, routers, and IP address translations. Here, we simulate that idea simply.

Next, we’ll allow access from this external network to internal services like:

HTTP (80)

MySQL (3306)

SSH (4422)

🔧 Steps:
Start your firewall VM and log in.

Go to:
Firewall > NAT > Port Forward

Add rules like so:

| Source Port | Destination (Internal) IP | Destination Port |
|-------------|----------------------------|------------------|
| 80          | 10.0.20.10                 | 80               |
| 3306        | 10.0.20.10                 | 3306             |
| 4422        | 10.0.20.10                 | 22               |


> ⚠️ Port 4422 is used here for SSH instead of the default 22. Some consider it a basic security measure (obscurity), but it’s not a true defense.

## 🔍 Test Connectivity
Now let’s test whether our Kali Linux machine can connect to the internal network.

🌐 1. Web Access
Open a browser inside Kali and go to:

```
http://10.0.10.254
```
You should see the DVWA homepage.

🔐 2. SSH
Try initiating an SSH connection:
```
ssh -p 4422 user@10.0.20.10
```
(You can cancel before entering credentials)

🛢️ 3. MySQL Access
Test the MariaDB connection (e.g., using mysql or a scanning tool) to ensure port 3306 is open.

## ✅ Summary
That’s it for today!

We now have a malicious machine inside our Racoon network for testing attacks and monitoring how our internal defenses respond.

Down the road, we may add more offensive tools if Kali’s default toolkit isn’t enough.

Next up:
We’ll (finally) start deploying our SIEM solution—we’ll be using Security Onion. Stay tuned! 🧅

Until next time—keep testing, keep hardening. 💪
