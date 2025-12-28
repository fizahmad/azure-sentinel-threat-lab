# Windows VM Setup

## VM Configuration

Created a Windows 10 Pro VM in VMware Workstation with the following specs: 

| Setting | Value |
|---------|-------|
| RAM | 4 GB |
| CPUs | 2 |
| Disk | 60 GB |
| Network | NAT |

<p align="center">
  <img width="700" height="450" alt="windows-vm"
       src="https://github.com/user-attachments/assets/90ab2662-b00b-4a62-aa5e-fa3dc30ddb85">
</p>

<p align="center"><em>Figure: Windows 10 Pro VM</em></p>

## Sysmon Installation

Sysmon provides detailed logging for process creation, network connections, and file changes.

**Download:** https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

**Install:**
```powershell
.\Sysmon64.exe -accepteula -i
```

Verify installation in Event Viewer: 

<p align="center">
  <img width="700" height="450" alt="Sysmon Logs"
       src="https://github.com/user-attachments/assets/88054995-ef00-4d9e-94d6-6ed810dfee20">
</p>

<p align="center"><em>Figure: Sysmon Logs in Windows Event Viewer</em></p>

## PowerShell Logging

Enabled script block logging to capture PowerShell commands. 

**Path:** `gpedit.msc` > Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell

**Enable:** "Turn on PowerShell Script Block Logging"

<p align="center">
  <img width="700" height="450" alt="PowerShell Logging"
       src="https://github.com/user-attachments/assets/edf12998-9688-4d26-a477-a232e33a0b95">
</p>

<p align="center"><em>Figure: PowerShell Logging Enabled</em></p>

Next: [Sentinel Onboarding](./sentinel_windows_onboarding.md)
