# Kali Linux VM Setup (Attacker Machine)

This document outlines how I prepared a Kali Linux virtual machine to simulate attacks in the lab.

## 1. Create Kali VM in VirtualBox
- Downloaded latest Kali ISO from [official site](https://www.kali.org/get-kali/).
- Created a new VM with:
  - 2GB RAM, 1 vCPU
  - Bridged Adapter
  - 25GB storage

## 2. Tools Installed
Kali ships with most offensive tools preinstalled. Additionally, installed:
- `nmap`, `impacket`, `evil-winrm`, `crackmapexec`, `bloodhound`, etc.


## 3. Networking & SSH
- Verified network reachability to the Windows VM.
- Enabled OpenSSH for remote access.


This VM is used to simulate credential access, lateral movement, and other MITRE ATT&CK TTPs.
