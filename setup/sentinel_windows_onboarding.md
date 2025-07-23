# Windows VM Log Ingestion via Azure Arc & Microsoft Sentinel

## Objective

Connect a non-Azure Windows 10 VM (running locally on VirtualBox) to Microsoft Sentinel for real-time log ingestion and threat detection **without hosting the VM in Azure**.

This was achieved using **Azure Arc**, **Log Analytics**, and a **Data Collection Rule (DCR)** to collect Security, System, and Application logs.

## Components Used

| Component | Purpose |
|----------|---------|
| **Azure Arc** | Onboards non-Azure machines for Azure management |
| **Data Collection Rule (DCR)** | Defines which logs to collect |
| **Azure Monitor Agent (AMA)** | Forwards logs to Azure |
| **Log Analytics Workspace** | Acts as the data store for logs, which Microsoft Sentinel processes for detection and investigation. |
| **Microsoft Sentinel** | SIEM layer for detection rules and investigations |


## Summary Workflow

| Step | Description |
|------|-------------|
| 1️⃣ | Onboard VM with Azure Arc |
| 2️⃣ | Create Log Analytics Workspace + Enable Sentinel |
| 3️⃣ | Configure DCR (Security, System, Application logs) |
| 4️⃣ | Assign VM to DCR (Auto-installs AMA) |
| 5️⃣ | Logs start flowing to Sentinel |


## Setup Steps

### 1. Onboard Windows VM via Azure Arc

- Downloaded onboarding script from Azure Arc > Servers
- Ran script in **elevated PowerShell** on the VM

Ref: [arc-onboarding-script.png](./screenshots/arc-onboarding-script.png)

- Verified VM appears in **Azure Arc > Machines**

Ref: [arc-onboarded-machine.png](./screenshots/arc-onboarded-machine.png)

### 2. Create Log Analytics Workspace + Enable Sentinel

- Created a new **Log Analytics Workspace**

Ref: [log_analytics_workspace.png](./screenshots/log_analytics_workspace.png)

- Enabled **Microsoft Sentinel** on the same workspace

Ref: [sentinel_enabled.png](./screenshots/sentinel_enabled.png)

### 3. Create a Data Collection Rule (DCR)

- Target: **Windows Platform**
- Collected Logs:
  - `Security`
  - `System`
  - `Application`
- Destination: The same workspace as Sentinel

Ref: [dcr_created.png](./screenshots/dcr_created.png)

### 4. Assign DCR to Arc-Connected VM

- Added the VM as a **target resource**
- Azure pushed the **Azure Monitor Agent** automatically

### 5. Confirm Logs in Sentinel

Verified the logs are Available under **Sentinel > Logs**

Ref: [sentinel_logs_confirmed.png](./screenshots/sentinel_logs_confirmed.png)

## Why Azure Arc?

Local VMs (like those in VirtualBox) can’t be onboarded like Azure-native VMs. Azure Arc bridges this gap **treating local or on-prem machines as first-class Azure resources**.

Benefits:
- Enables cloud-native monitoring
- Applies Azure policies and extensions
- Integrates directly with Sentinel

## Outcome

My VirtualBox-hosted Windows VM is now feeding logs into Microsoft Sentinel as if it were an Azure VM, fully enabling detection rule testing, hunting, and playbook simulations as part of this SOC lab.