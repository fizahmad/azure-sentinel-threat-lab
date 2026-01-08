# Detection Rules

Custom KQL detection rules for Microsoft Sentinel.  Each rule maps to MITRE ATT&CK and works with the log parsers in `parsers/`.

## Prerequisites

Before using these rules, deploy the parser functions from `parsers/`:
- `SysmonParsed` - for Sysmon-based detections
- `PowerShellParsed` - for PowerShell log detections

## Rules Overview

| ID | Name | MITRE | Severity | Data Source |
|----|------|-------|----------|-------------|
| 001 | LSASS Memory Dump | T1003.001 | High | Sysmon EID 10 |
| 002 | PowerShell Encoded Command | T1059.001 | High | SecurityEvent 4688 |
| 003 | Rundll32 Suspicious Execution | T1218.011 | Medium | Sysmon EID 1 |
| 004 | Scheduled Task Persistence | T1053.005 | Medium | Sysmon EID 1 |
| 005 | SMB Lateral Movement | T1021.002 | High | Sysmon EID 3 |
| 006 | WMI Process Creation | T1047 | Medium | Sysmon EID 1 |
| 007 | RDP Brute Force | T1110.001 | High | SecurityEvent 4625 |
| 008 | PsExec Service Creation | T1021.002 | High | SecurityEvent 7045 |
| 009 | New Local Admin | T1098 | High | SecurityEvent 4732 |
| 010 | PowerShell Download | T1059.001 | High | Sysmon EID 1 |
| 011 | AMSI Bypass | T1562.001 | High | Sysmon EID 1 |
| 012 | SAM Database Copy | T1003.002 | High | Sysmon EID 1 |
| 013 | Defender Disabled | T1562.001 | High | Sysmon EID 1 |
| 014 | Registry Run Key Persistence | T1547.001 | Medium | Sysmon EID 13 |
| 015 | Shadow Copy Deletion | T1490 | High | Sysmon EID 1 |
| 016 | WMI Persistence | T1546.003 | Medium | Sysmon EID 19/20/21 |
| 017 | WinRM Remoting | T1021.006 | Medium | Sysmon EID 1 |
| 018 | SMB File Copy | T1021.002 | High | Sysmon EID 11 |
| 019 | LSASS Handle Access Spike | T1003.001 | High | Sysmon EID 10 |
| 020 | Office Child Process | T1204.002 | High | Sysmon EID 1 |
| 021 | DCSync | T1003.006 | Critical | SecurityEvent 4662 |

## By MITRE Tactic

### Execution
- 002 - PowerShell Encoded Command
- 003 - Rundll32 Suspicious Execution
- 010 - PowerShell Download
- 020 - Office Child Process

### Credential Access
- 001 - LSASS Memory Dump
- 007 - RDP Brute Force
- 012 - SAM Database Copy
- 019 - LSASS Handle Access Spike
- 021 - DCSync

### Lateral Movement
- 005 - SMB Lateral Movement
- 006 - WMI Process Creation
- 008 - PsExec Service Creation
- 017 - WinRM Remoting
- 018 - SMB File Copy

### Persistence
- 004 - Scheduled Task Persistence
- 009 - New Local Admin
- 014 - Registry Run Key Persistence
- 016 - WMI Persistence

### Defense Evasion
- 011 - AMSI Bypass
- 013 - Defender Disabled

### Impact
- 015 - Shadow Copy Deletion

## How to Import

1. Go to **Sentinel > Analytics > Create > Scheduled query rule**
2. Copy values from YAML file: 
   - Name, Description, Severity
   - MITRE tactics/techniques
   - Query
   - Frequency and period (1h)
3. Click **Review + create**

## Testing

Use commands from `attack-simulation/README.md` to trigger each rule in your lab. 