# Detection Rules (KQL)

This folder contains custom detection queries written in KQL (Kusto Query Language) for Microsoft Sentinel.

Each rule maps to a specific MITRE ATT&CK technique and is designed to be triggered by attack behaviors executed in the `attack-simulation` environment.

## Included Detection Rules

### **Execution**
- `PowerShell_EncodedCommand.kql`  
  - Detects encoded or obfuscated PowerShell execution  
  - **MITRE:** T1059.001  
  - **Trigger:** Atomic Red Team → `Invoke-AtomicTest T1059.001`

- `rundll32_suspicious_execution.kql`  
  - Detects LOLBin abuse via Rundll32 executing scripts  
  - **MITRE:** T1218.011  
  - **Trigger:** Rundll32 with `.js` / `.vbs` payloads

### **Credential Access**
- `LSASS_Memory_Dump.kql`  
  - Detects LSASS memory access from non-system processes  
  - **MITRE:** T1003.001  
  - **Trigger:** Procdump, Mimikatz, comsvcs.dll

### **Lateral Movement**
- `SMB_LateralMovement.kql`  
  - Detects remote access to ADMIN$, C$, IPC$  
  - **MITRE:** T1021.002  
  - **Trigger:** PsExec, copy over SMB, admin share access

- `wmi_process_creation_suspicious.kql`  
  - Detects WMI-based remote execution  
  - **MITRE:** T1047  
  - **Trigger:** `wmic process call create "cmd.exe /c calc.exe"`

### **Persistence**
- `scheduled_task_creation_persistence.kql`  
  - Detects creation of new scheduled tasks (Windows Event 4698)  
  - **MITRE:** T1053.005  
  - **Trigger:** `schtasks.exe /create /tn backdoor /tr ...`