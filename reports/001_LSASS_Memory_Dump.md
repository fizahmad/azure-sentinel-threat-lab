# 001 - LSASS Memory Dump

## What this is
This report documents the lab validation for Detection Rule **001**.

- **Detection file:** `detections/001-lsass-memory-dump.yaml`
- **Simulation guide:** `attack-simulation/001-LSASS-Memory-Dump-Simulation.MD` 

## Goal
Trigger the detection by dumping `lsass.exe` using ProcDump on the Windows lab VM, then capture evidence (logs + incident) in Microsoft Sentinel.

## Lab steps 

### Step 1: Confirm Sysmon is ingesting (Sentinel Logs)
Run:

```kql
WindowsEvent
| where TimeGenerated > ago(30m)
| where Provider == "Microsoft-Windows-Sysmon"
| summarize count() by EventID
| order by EventID asc
```

You should see Event IDs (ex: 1, 10, 11, 13). If you see **no Sysmon events**, stop and fix ingestion before continuing.

<p align="center">
  <img width="700" height="450" alt="Logs Summary"
       src="HERE SSS 1">
</p>

<p align="center"><em>Figure: Logs Summary</em></p>

---

### Step 2: Create/Enable the Analytic Rule (Rule 001)
In Azure Portal:
1. Microsoft Sentinel → your workspace
2. Analytics → Create → Scheduled query rule
3. Copy the query + settings from: `detections/001-lsass-memory-dump.yaml`
4. Enable incident creation

**Screenshot (SS1):** Rule 001 configuration page (show name + query + schedule).

---

### Step 3 — Run the attack simulation (Windows VM)
On the Windows VM (PowerShell **Run as Administrator**), run the Rule 001 commands from:
- `attack-simulation/README.md` → **Rule 001 — LSASS Memory Dump (ProcDump)**

**Screenshot (SS2 optional):** The PowerShell window showing the command execution.

---

### Step 4 — Validate logs in Sentinel (must-do)
In Sentinel → Logs, run this:

```kql
WindowsEvent
| where TimeGenerated > ago(1h)
| where Provider == "Microsoft-Windows-Sysmon"
| where EventID == 1
| extend Image=tostring(EventData.Image),
         CommandLine=tostring(EventData.CommandLine),
         ParentImage=tostring(EventData.ParentImage),
         User=tostring(EventData.User)
| where Image has "\\procdump" and CommandLine has "lsass"
| project TimeGenerated, Computer, User, Image, CommandLine, ParentImage
| order by TimeGenerated desc
```

**Screenshot (SS3):** Log results row showing `procdump.exe` with `lsass` in the command line.

---

### Step 5 — Confirm incident in Sentinel
1. Sentinel → Incidents
2. Open the incident created by Rule 001

**Screenshot (SS4):** Incidents list showing the new incident.  
**Screenshot (SS5):** Incident details page showing entities/evidence.

---

### Step 6 — Cleanup (Windows VM)
Run the cleanup commands from:
- `attack-simulation/README.md` → Rule 001 cleanup

**Screenshot (optional):** File removed / cleanup confirmation.

---

## Evidence
> Put images in the repo (example: `reports/screenshots/`) and reference them here.

### SS1 — Rule config
(attach image)

### SS3 — Sysmon EID 1 log evidence (ProcDump + lsass)
(attach image)

### SS4 — Sentinel incident created
(attach image)

### SS5 — Incident details
(attach image)