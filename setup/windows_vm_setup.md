# Connecting Windows Device to Sentinel

**1. Create VM**
- Downloaded a Windows 10 ISO.
- Created a new Virtual Machine in **VMware Workstation 17 Pro** with:
  - 4GB RAM, 2 vCPUs
  - Guest Additions installed
<img width="860" height="410" alt="Windows" src="https://github.com/user-attachments/assets/f74740e2-46e2-4f49-8653-c0d15e9df015" />
<p align="center"> Figure: Windows 10 Pro VM </p>                                              

**2. Enable Required Logging**
- Enabled the following Event Log channels:
  - Security
  - System
  - Application
  - Windows PowerShell
  - Sysmon
- Installed and configured **Sysmon** for detailed process/network tracking. [Ref to Setup Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
<img width="860" height="410" alt="2025-11-20_03-22" src="https://github.com/user-attachments/assets/88054995-ef00-4d9e-94d6-6ed810dfee20" />
<p align="center"> Figure: Sysmon Logs in Windows Event Viewer </p>

**3. Azure Arc Agent Installation**
- Download the onboarding script from Azure Arc
- Run it in powershell.
<img width="860" height="410" alt="2025-11-20_03-34" src="https://github.com/user-attachments/assets/2468f827-f99a-4147-87d3-83ab8bc6ce61" />
<p align="center"> Figure: Windows Device is Added to Azure Arc </p>

**Next:** [sentinel_windows_onboarding.md](./sentinel_windows_onboarding.md)
