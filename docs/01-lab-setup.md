# Phase 1 - Lab Environment Setup

## Overview

The first phase of this project focused on creating the virtual infrastructure for the cybersecurity home lab. Oracle VirtualBox was used to deploy a Windows Server 2025 virtual machine that will later function as an Active Directory domain controller.

## Host System

The lab is hosted on a Windows computer with the following hardware:

- Intel Core i5-10400
- 16 GB RAM
- SSD storage
- Intel hardware virtualization enabled

## Virtualization

Oracle VirtualBox was selected as the virtualization platform for the lab.

The first virtual machine was configured with:

| Setting | Configuration |
|---|---|
| VM Name | DC01 |
| Operating System | Windows Server 2025 Standard Evaluation |
| Memory | 4 GB |
| Processors | 2 |
| Virtual Disk | 50 GB dynamically allocated |
| Adapter 1 | NAT |
| Adapter 2 | Internal Network (CYBER-LAB) |

## Server Configuration

The Windows Server hostname was changed to:

`DC01`

The name identifies the system as the first domain controller in the lab environment.

## Network Architecture

DC01 contains two virtual network interfaces.

### NAT-INTERNET

The NAT interface provides external network and internet connectivity through VirtualBox.

### CYBER-LAB

The second interface connects DC01 to an isolated VirtualBox internal network named:

`CYBER-LAB`

A static IPv4 address was assigned to this interface:

- IP Address: `10.0.0.10`
- Prefix Length: `/24`
- Subnet Mask: `255.255.255.0`
- Default Gateway: None

The internal network will eventually connect the Windows workstation, Linux server, and security testing systems.

## Network Design

Internet
|
VirtualBox NAT
|
DC01
|
10.0.0.10/24
|
CYBER-LAB
|
+---------+---------+
|         |         |
CLIENT01  UBUNTU01  KALI01

## Verification

Network configuration was verified using PowerShell and Windows networking utilities:

`Get-NetAdapter`

`ipconfig`

Internet connectivity and DNS resolution were also tested from DC01.
