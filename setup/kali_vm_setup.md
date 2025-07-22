# Kali Linux VM Setup

This document outlines the setup process for the Kali Linux virtual machine, which will be used to simulate real-world adversarial behavior in the Azure Sentinel Threat Detection Lab. The Kali VM acts as the attacker machine in this environment.

## 1. VM Environment

- **Hypervisor**: Oracle VirtualBox 7.0.22
- **ISO Used**: `kali-linux-2024.4-virtualbox-amd64.iso`
- **VM Specs**:
  - CPU: 2 vCPUs
  - RAM: 4 GB (will increase later, if needed)
  - Disk: 25 GB (Dynamically allocated)
  - Network: NAT (for internet access)

## 2. Installation & Basic Configuration

1. **Install Kali Linux**
   - Download the official ISO from [kali.org](https://www.kali.org/get-kali/)
   - Create a new VM in VirtualBox and attach the ISO
   - Complete a standard guided install (Graphical install)

2. **Post-Install Setup**
   - Update system packages:
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```

## 3. Tools Installation (To Be Done Per Attack Simulation)

No unnecessary tools are preinstalled at this stage. Relevant tools will be installed **only during each attack simulation phase** under `attack-simulation/`.

Example categories:
- Credential access tools
- Network scanning utilities
- Post-exploitation frameworks
- Payload generators

Each will be documented with:
- Purpose
- TTP mapping (MITRE ATT&CK)
- Commands used

## 4. Lab Role

The Kali VM will:
- Initiate attacks (brute force, lateral movement, enumeration)
- Simulate common threat actor behavior against the Windows VM
- Help validate custom detections and playbooks in Microsoft Sentinel