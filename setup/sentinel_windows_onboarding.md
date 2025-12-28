# Connecting Windows VM to Sentinel

Azure Arc enables local VMs to send logs to Azure without hosting them in the cloud.

## Components Used

| Component | Purpose |
|----------|---------|
| **Azure Arc** | Onboards non-Azure machines for Azure management |
| **Data Collection Rule (DCR)** | Defines which logs to collect |
| **Azure Monitor Agent (AMA)** | Forwards logs to Azure |
| **Log Analytics Workspace** | Acts as the data store for logs, which Microsoft Sentinel processes for detection and investigation. |
| **Microsoft Sentinel** | SIEM layer for detection rules and investigations |

## Why Azure Arc?

Local VMs can’t be onboarded like Azure-native VMs. Azure Arc bridges this gap **treating local or on-prem machines as first-class Azure resources**.

Benefits:
- Enables cloud-native monitoring
- Applies Azure policies and extensions
- Integrates directly with Sentinel

## Azure Arc Agent

**Portal:** Azure Arc > Infrastructure > Machines > Onboard/Create > Onboard Existing Machines > Generate script

Download and run the script on the Windows VM as Administrator.

<p align="center">
  <img width="700" height="450" alt="Arc Script Download"
       src="https://github.com/user-attachments/assets/933a68f5-38e2-4622-be89-8839af6d09f4">
</p>
<p align="center"><em>Figure: Arc Script Download</em></p>

<br>

<p align="center">
  <img width="700" height="450" alt="Arc Agent Installing"
       src="https://github.com/user-attachments/assets/415ae5d3-9dac-4514-8116-4f779505c584">
</p>
<p align="center"><em>Figure: Arc Agent Installing</em></p>

After installation, the VM appears in Azure Arc: 

<p align="center">
  <img width="700" height="450" alt="VM in Azure Arc"
       src="https://github.com/user-attachments/assets/4a14270f-afe2-46cf-89bf-656fa524f48a">
</p>

<p align="center"><em>Figure: VM in Azure Arc</em></p>

## Data Collection Rule

Configure which logs to collect from the VM. 

**Portal:** Data Collection Rules > Create

| Setting | Value |
|---------|-------|
| Platform | Windows |
| Resources | Select Arc-connected VM |
| Data Sources | Security, System, Application, Sysmon |

![Data Collection Rule](./dcr_created.png)

The Azure Monitor Agent installs automatically when the rule is applied.

## Verify Log Ingestion

After 10-15 minutes, test log flow in Sentinel. 

**Portal:** Sentinel > Logs

```kql
SecurityEvent
| take 10
```

![Security Logs](./security_logs_test.png)

```kql
SysmonEvent
| take 10
```

![Sysmon Logs](./sysmon_logs_test. png)

Setup complete. The VM is now sending logs to Sentinel. 

