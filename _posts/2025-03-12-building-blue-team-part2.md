---
title: 'Building Blue Team Home Lab - Part 2 : Network Topology'
date: 2025-03-12
permalink: /posts/2025/03/building-blue-team-part2/
tags:
  - Blue Team
  - Home Lab
---

### Introduction
Welcome to Part 2 of my Blue Team Home Lab series! In this post, we’ll dive into the **network topology** and **VLAN design** that power a secure, flexible, and scalable cyber defense lab.

---

### Quick Recap

In Part 1, we talked about:
- Why I built a home lab
- The tools I’m using
- My PC specs and setup

Now it’s time to lay out the **networking foundation** for everything that follows.

---

### Design Goals

Before spinning up VMs, I created a list of what I want to do in this lab:
- SIEM
- Malware Analysis (Linux & Windows)
- DFIR & OSINT
- Email Forensics
- Vulnerability Scanning
- Active Directory, Proxy, IDS/IPS, Monitoring, etc.

This helped shape the topology and host selection.

---

### Core Hosts and Services

Planned hosts include:

- `Firewall`
- `Windows 7` & `Windows 10`
- `Windows Server AD`
- `Linux Servers`
- `Kali Linux`
- `DFIR & Malware Analysis VMs`
- `SIEM`
- `Vulnerability Scanner`

Planned services:

- Antivirus / EDR / XDR
- Proxy, Mail Server
- AD, IDS/IPS
- Docker, Databases
- Monitoring tools

> Many of these can run on the same VM or shared infrastructure.

---

### VLAN & Subnet Planning

The lab will use **VLAN segmentation** for security and clarity. Here’s the setup:

| **Name**           | **Domain**        | **VLAN** | **Subnet**         | **Gateway**       |
|--------------------|-------------------|----------|---------------------|-------------------|
| Management         | N/A               | 1        | `10.0.1.0/24`       | `10.0.1.1`        |
| Corporate WAN      | N/A               | 10       | `10.0.10.0/24`      | `10.0.10.254`     |
| Corporate LAN      | cyber.hub         | 20       | `10.0.20.0/24`      | `10.0.20.254`     |
| Security VLAN      | cyber.hub         | 50       | `10.0.50.0/24`      | `10.0.50.254`     |
| Isolated Malware   | N/A               | 99       | `10.0.99.0/24`      | `10.0.99.254`     |

Each VLAN represents a distinct zone:
- VLAN 1: Management GUI access
- VLAN 10: Fake WAN (simulated internet/Kali Linux)
- VLAN 20: Internal users (Windows 7/10, AD)
- VLAN 50: Security team (with outbound access)
- VLAN 99: Fully isolated malware analysis

---

### VLAN Creation in VMware

If you're using **VMware Workstation Pro**:

1. Go to **Edit → Virtual Network Editor**
2. Add 4 new networks (`vmnet10`, `vmnet20`, `vmnet50`, `vmnet99`)
3. Uncheck **Use local DHCP service**
4. Set each subnet manually according to the table above
5. Keep them as **host-only networks**

---

### Final Topology

The resulting topology looks something like this (drawn using [draw.io](https://draw.io)):

![Network Diagram](/images/net.drawio.png)
> A segmented, multi-VLAN lab that mimics a real-world corporate network with external threats, internal systems, and blue team defenses.

---

### Summary

- We defined **network segments** via VLANs
- Planned IP addressing and host types
- Set up isolated zones for analysis and monitoring
- Created a flexible, evolving base for the lab

---

### Reference

This post was inspired by and adapted from:

[Blue Team Lab Guide - Part 2 by Marko Andrejic](https://facyber.me/posts/blue-team-lab-guide-part-2/)

---

In the next part, we’ll start **deploying virtual machines** and configuring the firewall. Stay tuned and happy labbing!
