# Windows VM Setup (Victim/Target Machine)

This document explains how I prepared a Windows 10 Pro virtual machine to simulate endpoint activity in the Sentinel lab.

## 1. Create VM in VirtualBox
- Downloaded a clean Windows 10 ISO.
- Created a new Virtual Machine in **VirtualBox 7.0.22** with:
  - 4GB RAM, 2 vCPUs
  - Guest Additions installed

Ref: [windowsVM-target.png](./screenshots/windowsVM-target.png)

## 2. Enable Required Logging
- Enabled the following Event Log channels:
  - Security
  - System
  - Application
  - Windows PowerShell
  - Sysmon
- Installed and configured **Sysmon** with a curated config for detailed process/network tracking.

## 3. Configure Windows Firewall and Defender
- Ensured Windows Firewall is enabled and logs both allowed and blocked connections.
- Added exclusions for lab tools (e.g., Sysmon, WinLogBeat).

## 4. Azure Arc Agent Installation
- Downloaded onboarding script from Azure Arc and run it in powershell.

Ref: [arc-onboarding-script.png](./screenshots/arc-onboarding-script.png)

- Connected the VM using the script.

Ref: [arc-onboarded-machine.png](./screenshots/arc-onboarded-machine.png)


**Next:** [sentinel_windows_onboarding.md](./sentinel_windows_onboarding.md)