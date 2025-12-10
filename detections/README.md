# Detection Rules (KQL → Sentinel Analytic Rules)

This folder contains custom detection queries as Sentinel analytic rule templates. Each rule maps to MITRE ATT&CK and aligns with behaviors in `attack-simulation/`.

## Included Detection Rules

### Execution / Defense Evasion
- `002_PowerShell_EncodedCommand.yaml` — Encoded/obfuscated PowerShell (T1059.001)
- `003_rundll32_suspicious_execution.yaml` — Rundll32 launching scripts/URLs (T1218.011)
- `010_Suspicious_PowerShell_Download.yaml` — IEX/IWR/DownloadString staging (T1059.001)
- `011_PowerShell_AMSI_Bypass.yaml` — AMSI bypass strings (T1562.001)
- `020_Suspicious_Child_Of_Office.yaml` — Office spawning scripting/PowerShell (T1204.002)
- `013_Defender_Disable_Settings.yaml` — PowerShell disabling Defender (T1562.001)

### Credential Access
- `001_LSASS_Memory_Dump.yaml` — LSASS memory access (T1003.001)
- `019_Lsass_Handle_Access_Sysmon10.yaml` — LSASS handle spike (T1003.001)
- `012_SAM_Database_Copy.yaml` — `reg save HKLM\SAM` (T1003.002)
- `021_DCSync_Replication_Request.yaml` — DCSync replication from non-DC (T1003.006)
- `007_RDP_BruteForce_LogonFailures.yaml` — Multiple 4625 RDP failures (T1110.001)

### Lateral Movement
- `005_SMB_LateralMovement.yaml` — Admin share connections (T1021.002)
- `008_PsExec_Service_Creation.yaml` — PSEXESVC service creation (T1021.002)
- `018_SMBexec_Admin_Share_Copy.yaml` — File copy into admin shares (T1021.002)
- `017_Remote_PowerShell_Remoting.yaml` — WinRM wsmprovhost child (T1021.006)
- `006_wmi_process_creation_suspicious.yaml` — WMI remote process (T1047)

### Persistence / Privilege Escalation
- `004_scheduled_task_creation_persistence.yaml` — New scheduled task (T1053.005)
- `009_New_Local_Admin_Account.yaml` — New user added to Administrators (T1098)
- `014_Registry_RunKey_Persistence.yaml` — Run/RunOnce modifications (T1547.001)
- `016_Suspicious_WMI_Persistence.yaml` — WMI event subscription (T1546.003)

### Impact
- `015_VSSAdmin_Delete_Shadows.yaml` — Shadow copy deletion (T1490)

> Use these with Sentinel’s Scheduled analytic rules. Each YAML already includes `queryFrequency`, `queryPeriod`, severity, MITRE mapping, and connector hints.