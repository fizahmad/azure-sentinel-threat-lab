# Windows Log Ingestion Setup – Sentinel + Azure Arc

## Overview

In this section, I explain how I connected my **non-Azure Windows 10 VM (Victim/target)** to Microsoft Sentinel. Since the machine is running locally in VirtualBox, I used **Azure Arc** to bring it under Azure management. This enabled me to collect security logs into Sentinel for threat detection.

## Key Components Used

| Component | Purpose |
|----------|---------|
| **Azure Arc** | Allows onboarding of non-Azure machines into Azure management. I used it to connect my VirtualBox-based Windows 10 VM. |
| **Data Collection Rule (DCR)** | A policy that tells Azure what types of logs to collect and from which machines. I configured it to collect `Security`, `System`, and `Application` logs. |
| **Azure Monitor Agent (AMA)** | Automatically deployed on the VM once it's associated with a DCR. This agent sends the logs to Azure. |
| **Log Analytics Workspace** | A storage layer where all logs are ingested before Sentinel analyzes them. I connected my VM to the same workspace where Sentinel is enabled. |
| **Microsoft Sentinel** | The SIEM platform I’m using to visualize logs, write detection rules, and simulate SOC operations. |

## Summary

| Step | Action | Why I Did It |
| --- | --- | --- |
| 1️⃣ | Onboarded VM using Azure Arc | So Azure could manage my non-Azure machine |
| 2️⃣ | Created a Data Collection Rule | To specify the types of logs to collect |
| 3️⃣ | Associated the VM to the DCR | So logs could start flowing |
| 4️⃣ | Logs appeared in Sentinel | Ready for detection rules and KQL hunting |

## End-to-End Flow

1. I onboarded my VM using **Azure Arc** and confirmed it appeared under *Azure Arc > Servers*.
2. I created a **Log Analytics Workspace** and enabled **Microsoft Sentinel** on it.
3. I created a **Data Collection Rule (DCR)** that collects:
   - Windows Security Events
   - System Logs
   - Application Logs
4. I associated the DCR with my Arc-connected VM.
5. Azure automatically installed the **Azure Monitor Agent** via extension.
6. Logs started appearing under Sentinel's “Logs” blade (`SecurityEvent`, `Event`, etc.).

## Why I Used Azure Arc

Since my Windows 10 machine is hosted locally in VirtualBox and **not in Azure**, it cannot natively send logs to Sentinel like an Azure VM would. Azure Arc solves this problem by treating my on-prem (or local) machine *as if* it were an Azure resource.

This lets me:
- Remotely manage the VM
- Apply monitoring policies
- Collect logs using Azure-native services

## Step-by-Step Breakdown

### 🔴 Step 1 – Connect VM to Azure using Azure Arc

I downloaded the PowerShell onboarding script for Windows machines from the Azure Arc portal, ran it in an **elevated PowerShell session** on my victim VM, and verified that the VM appeared in the Azure Arc resource list.

`screenshots/azure_arc_script_execution.png`

### 🔵 Step 2 – Create Data Collection Rule (DCR)

From within Azure Monitor, I created a new DCR with:
- Platform: **Windows**
- Logs to collect: **Security**, **System**, and **Application**
- Destination: My Log Analytics Workspace used by Sentinel

`screenshots/dcr_creation_wizard.png`

### 🟣 Step 3 – Associate DCR to VM

I added my Arc-connected VM as a **target machine** for the DCR. Azure automatically pushed the **Azure Monitor Agent** as an extension.

`screenshots/dcr_vm_assignment.png`

### Step 4 – Logs Start Flowing into Sentinel

After a few minutes, I confirmed logs were arriving:
- `SecurityEvent`
- `Event`
- `Heartbeat` (from AMA)

`screenshots/sentinel_logs_confirmed.png`

---

Using Azure Arc + DCR + AMA allowed me to **treat a local VirtualBox VM like a native Azure resource**, enabling log ingestion directly into Microsoft Sentinel.

This completes the **log onboarding phase** of this SOC lab.
