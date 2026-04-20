# 003 - Rundll32 Suspicious Script Execution

## What this is
This report documents the lab validation for Detection Rule **003**.

- **Detection file:** [`detections/003_rundll32_suspicious_execution.yaml`](/detections/003_rundll32_suspicious_execution.yaml)
- **Simulation guide:** [`attack-simulation/003-Rundll32-Suspicious-Execution.md`](/attack-simulation/003-Rundll32-Suspicious-Execution.md)

## Goal
Trigger the detection by executing `rundll32.exe` with suspicious script/URL handler patterns (ex: `javascript:` / `mshtml`), then capture evidence (logs + incident) in Microsoft Sentinel.

## Lab steps

### Step 1: Confirm 4688 process creation events are ingesting (Sentinel Logs)
Run:

```kql
SecurityEvent
| where TimeGenerated > ago(30m)
| summarize count() by EventID
| order by EventID asc
```

You should see Event ID **4688**. If you see **no 4688 events**, stop and fix Windows Security auditing / ingestion before continuing.

<p align="center">
  <img width="850" height="450" alt="SecurityEvent Summary (4688 present)"
       src="PASTE_YOUR_SCREENSHOT_LINK_HERE">
</p>

<p align="center"><em>Figure: SecurityEvent Summary (4688 present)</em></p>

### Step 2: Create/Enable the Analytic Rule (Rule 003)
In Azure Portal:
1. Microsoft Sentinel → your workspace
2. Analytics → Create → Scheduled query rule/NRT Rule
3. Copy the query + settings from: [`detections/003_rundll32_suspicious_execution.yaml`](/detections/003_rundll32_suspicious_execution.yaml)
4. Enable incident creation

<p align="center">
  <img width="850" height="450" alt="Rule 003 configuration page-1"
       src="PASTE_YOUR_SCREENSHOT_LINK_HERE">
</p>

<p align="center"><em>Figure: Rule 003 configuration page-1</em></p>

<p align="center">
  <img width="850" height="450" alt="Rule 003 configuration page-2"
       src="PASTE_YOUR_SCREENSHOT_LINK_HERE">
</p>

<p align="center"><em>Figure: Rule 003 configuration page-2</em></p>

### Step 3: Run the attack simulation (Windows VM)
- On the Windows VM
- Run the commands from: [`attack-simulation/003-Rundll32-Suspicious-Execution.md`](/attack-simulation/003-Rundll32-Suspicious-Execution.md)

<p align="center">
  <img width="850" height="450" alt="Rundll32 suspicious command execution"
       src="PASTE_YOUR_SCREENSHOT_LINK_HERE">
</p>

<p align="center"><em>Figure: Rundll32 suspicious command execution</em></p>

### Step 4: Validate logs in Sentinel
In Sentinel → Logs, run this:

```kql
SecurityEvent
| where TimeGenerated > ago(1h)
| where EventID == 4688
| where NewProcessName endswith "\\rundll32.exe"
| where CommandLine has_any ("javascript:", "vbscript:", "url.dll", "mshtml", ".sct", ".js", ".vbs", "RunHTMLApplication")
| project TimeGenerated, Computer, Account, NewProcessName, CommandLine, ParentProcessName
| order by TimeGenerated desc
```

<p align="center">
  <img width="850" height="450" alt="4688 events showing rundll32 suspicious execution"
       src="PASTE_YOUR_SCREENSHOT_LINK_HERE">
</p>

<p align="center"><em>Figure: 4688 events showing rundll32 suspicious execution</em></p>

### Step 5: Confirm incident in Sentinel
1. Sentinel → Incidents
2. Open the incident created by Rule 003

<p align="center">
  <img width="850" height="450" alt="Incidents list showing the new incident"
       src="PASTE_YOUR_SCREENSHOT_LINK_HERE">
</p>

<p align="center"><em>Figure: Incidents</em></p>

<p align="center">
  <img width="850" height="450" alt="Incident Details Page"
       src="PASTE_YOUR_SCREENSHOT_LINK_HERE">
</p>

<p align="center"><em>Figure: Incident Details Page</em></p>