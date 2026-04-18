## Rule 002 - PowerShell Encoded Command Execution (T1059.001)

### Purpose
Simulate encoded/obfuscated PowerShell execution using `-EncodedCommand` (Base64), commonly used by attackers to hide intent.

### Commands (Windows VM, PowerShell)
```powershell
# Build a command and encode using UTF-16LE (Unicode), which PowerShell expects for -EncodedCommand
$cmd = 'whoami; hostname; Get-Date'
$bytes = [System.Text.Encoding]::Unicode.GetBytes($cmd)
$b64 = [Convert]::ToBase64String($bytes)

# Execute with -EncodedCommand
powershell.exe -NoProfile -ExecutionPolicy Bypass -EncodedCommand $b64