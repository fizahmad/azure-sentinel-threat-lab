# 001 - LSASS Memory Dump

## What this is
This report documents the lab validation for Detection Rule **001**.

- **Detection file:** [`detections/001-lsass-memory-dump.yaml`](/detections/001-lsass-memory-dump.yaml)
- **Simulation guide:** [`attack-simulation/001-LSASS-Memory-Dump-Simulation.md`](/attack-simulation/001-LSASS-Memory-Dump-Simulation.md)

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
  <img width="850" height="450" alt="Logs Summary"
       src="https://github.com/user-attachments/assets/4b1d7266-7652-4e64-bd6c-385df0f75523">
</p>

<p align="center"><em>Figure: Logs Summary</em></p>

### Step 2: Create/Enable the Analytic Rule (Rule 001)
In Azure Portal:
1. Microsoft Sentinel → your workspace
2. Analytics → Create → Scheduled query rule
3. Copy the query + settings from: `detections/001-lsass-memory-dump.yaml`
4. Enable incident creation

<p align="center">
  <img width="850" height="450" alt="Rule 001 configuration page-1"
       src="https://github.com/user-attachments/assets/bbb5ad4e-4f53-4989-8d28-3c86b4cf1e52">
</p>

<p align="center"><em>Figure: Rule 001 configuration page-1</em></p>

<p align="center">
  <img width="850" height="450" alt="Rule 001 configuration page-2"
       src="https://github.com/user-attachments/assets/f6e21ced-4260-45c2-bfef-51a9b49e4d74">
</p>

<p align="center"><em>Figure: Rule 001 configuration page-2</em></p>

### Step 3: Run the attack simulation (Windows VM)
- On the Windows VM (PowerShell **Run as Administrator**)
- Run the commands from: [`attack-simulation/001-LSASS-Memory-Dump-Simulation.md`](/attack-simulation/001-LSASS-Memory-Dump-Simulation.md)

<p align="center">
  <img width="850" height="450" alt="PowerShell Command Execution"
       src="https://github.com/user-attachments/assets/282f2492-3316-459f-8118-a429f9ea823d">
</p>

<p align="center"><em>Figure: PowerShell Command Execution</em></p>

<p align="center">
  <img width="850" height="450" alt="Sysmon EID 1 log (ProcDump + lsass)"
       src="https://github.com/user-attachments/assets/19b17d87-c100-4d34-8dac-eb9366e20fa9">
</p>

<p align="center"><em>Figure: Sysmon EID 1 log (ProcDump + lsass)</em></p>

### Step 4: Validate logs in Sentinel
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
<p align="center">
  <img width="850" height="450" alt="Events"
       src="https://github.com/user-attachments/assets/e2e1701e-61d6-4142-96c4-0c80d0a7612f">
</p>

<p align="center"><em>Figure: Events</em></p>


### Step 5: Confirm incident in Sentinel
1. Sentinel → Incidents
2. Open the incident created by Rule 001

<p align="center">
  <img width="850" height="450" alt="Incidents list showing the new Incident"
       src="https://github.com/user-attachments/assets/ad812946-7c8f-4d47-b196-d25a62a1ecc3">
</p>

<p align="center"><em>Figure: Incidents</em></p>

<p align="center">
  <img width="850" height="450" alt="Incident Details Page"
       src="https://github.com/user-attachments/assets/74c0b237-bcf6-42f8-8173-0b16ae0cac49">
</p>

<p align="center"><em>Figure: Incident Details Page</em></p>