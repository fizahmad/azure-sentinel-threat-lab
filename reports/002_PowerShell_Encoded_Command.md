# 002 - PowerShell Encoded Command Execution

## What this is
This report documents the lab validation for Detection Rule **002**.

- **Detection file:** [`detections/002_PowerShell_EncodedCommand.yaml`](/detections/002_PowerShell_EncodedCommand.yaml)
- **Simulation guide:** [`attack-simulation/002-PowerShell-EncodedCommand.md`](/attack-simulation/002-PowerShell-EncodedCommand.md)

## Goal
Trigger the detection by executing PowerShell using a Base64 payload with `-EncodedCommand`, then capture evidence (logs + incident) in Microsoft Sentinel.

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
       src="https://github.com/user-attachments/assets/41338ba8-60b5-44e7-b672-6c547e6b3b7e">
</p>

<p align="center"><em>Figure: SecurityEvent Summary (4688 present)</em></p>

### Step 2: Create/Enable the Analytic Rule (Rule 002)
In Azure Portal:
1. Microsoft Sentinel → your workspace
2. Analytics → Create → Scheduled query rule/NRT Rule
3. Copy the query + settings from: [`detections/002_PowerShell_EncodedCommand.yaml`](/detections/002_PowerShell_EncodedCommand.yaml)
4. Enable incident creation

<p align="center">
  <img width="850" height="450" alt="Rule 002 configuration page-1"
       src="https://github.com/user-attachments/assets/55bb8179-d61a-4d4f-8fd0-08ac3532bb2c">
</p>

<p align="center"><em>Figure: Rule 002 configuration page-1</em></p>

<p align="center">
  <img width="850" height="450" alt="Rule 002 configuration page-2"
       src="https://github.com/user-attachments/assets/a409cc27-663c-429a-85d4-a9751acd99cb">
</p>

<p align="center"><em>Figure: Rule 002 configuration page-2</em></p>

### Step 3: Run the attack simulation (Windows VM)
- On the Windows VM
- Run the commands from: [`attack-simulation/002-PowerShell-EncodedCommand.md`](/attack-simulation/002-PowerShell-EncodedCommand.md)

<p align="center">
  <img width="850" height="450" alt="PowerShell EncodedCommand Execution"
       src="https://github.com/user-attachments/assets/fb05739c-92e5-4304-b486-48aa8a3f694e">
</p>

<p align="center"><em>Figure: PowerShell EncodedCommand Execution</em></p>

### Step 4: Validate logs in Sentinel
In Sentinel → Logs, run this:

```kql
SecurityEvent
| where TimeGenerated > ago(1h)
| where EventID == 4688
| where NewProcessName has_any ("\\powershell.exe", "\\pwsh.exe")
| where CommandLine has_any (" -enc ", " -encodedcommand ", "FromBase64String", " -e ")
| project TimeGenerated, Computer, Account, NewProcessName, CommandLine, ParentProcessName
| order by TimeGenerated desc
```

<p align="center">
  <img width="850" height="450" alt="4688 events showing EncodedCommand"
       src="https://github.com/user-attachments/assets/892403cf-c9e9-4daa-b884-f51cd236ef08">
</p>

<p align="center"><em>Figure: 4688 events showing EncodedCommand</em></p>

### Step 5: Confirm incident in Sentinel
1. Sentinel → Incidents
2. Open the incident created by Rule 002

<p align="center">
  <img width="850" height="450" alt="Incidents list showing the new incident"
       src="https://github.com/user-attachments/assets/c7d03542-a304-40d7-bd1a-aa79018bd1bb">
</p>

<p align="center"><em>Figure: Incidents</em></p>

<p align="center">
  <img width="850" height="450" alt="Incident Details Page"
       src="https://github.com/user-attachments/assets/2e99a684-8b4a-409e-98a6-f444a4605a6d">
</p>

<p align="center"><em>Figure: Incident Details Page</em></p>
