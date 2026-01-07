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

<p align="center">
  <img width="700" height="450" alt="Arc Agent Installing"
       src="https://github.com/user-attachments/assets/415ae5d3-9dac-4514-8116-4f779505c584">
</p>
<p align="center"><em>Figure: Arc Agent Installing</em></p>

<br>

After installation, the VM appears in Azure Arc: 

<br>

<p align="center">
  <img width="700" height="450" alt="VM in Azure Arc"
       src="https://github.com/user-attachments/assets/4a14270f-afe2-46cf-89bf-656fa524f48a">
</p>

<p align="center"><em>Figure: VM in Azure Arc</em></p>

## Configure the Data Connector

1. Go to **Microsoft Sentinel** > **Configuration** > **Data connectors**.
2. Select **Windows Security Events via AMA**.
3. Install the connector.
4. Click **Manage**.
5. Select **Windows Security Events via AMA**
6. Click **Open connector page**.

<p align="center">
  <img width="700" height="450" alt="Install the connector"
       src="https://github.com/user-attachments/assets/35516ea1-ccfc-44e1-b2c5-21cebad68d23">
</p>
<p align="center"><em>Figure: Install the connector</em></p>
<br>
<p align="center">
  <img width="700" height="450" alt="Open connector page"
       src="https://github.com/user-attachments/assets/51bbaab7-37da-4cfd-82b0-7897cf172b3a">
</p>
<p align="center"><em>Figure: Open connector page</em></p>

## Data Collection Rules

Two separate DCRs are required - one for Windows Security logs and another for Sysmon logs.

**Portal:** Sentinel > Data connectors > Windows Security Events via AMA > Open connector page

### DCR 1: Windows Security Events

#### Define Rule Details
1. Click **+ Create data collection rule**
2. Provide the following: 
   | Setting | Value |
   |---------|-------|
   | Rule Name | `WinSecurityEvents` |
   | Subscription | Select your subscription |
   | Resource Group | Select your lab resource group |

#### Add Target Machines
In the **Resources** tab, select the Windows VM to be monitored. 

#### Select Data to Collect
In the **Collect** tab:  
- Select **All Security Events**

Click **Review + create** to deploy the rule.

<p align="center">
  <img width="700" height="450" alt="WinSecurityEvents DCR"
       src="https://github.com/user-attachments/assets/4b409981-6836-4770-9474-8f8dcfc9808c">
</p>
<p align="center"><em>Figure: WinSecurityEvents DCR</em></p>


### DCR 2: Sysmon Logs

#### Define Rule Details
1. Click **+ Create data collection rule**
2. Provide the following:
   | Setting | Value |
   |---------|-------|
   | Rule Name | `WinSysmonLogs` |
   | Subscription | Select your subscription |
   | Resource Group | Select your lab resource group |

#### Add Target Machines
In the **Resources** tab, select the Windows VM to be monitored.

#### Select Data to Collect
In the **Collect** tab:
- Select **Custom**
- Enter the following in the text box and click **Add**:

```
Microsoft-Windows-Sysmon/Operational!*
```
Click **Review + create** to deploy the rule.

<p align="center">
  <img width="700" height="450" alt="WinSysmonLogs DCR"
       src="https://github.com/user-attachments/assets/532371a8-873f-4e1c-bf8a-d6db733f3647">
</p>
<p align="center"><em>Figure: WinSysmonLogs DCR</em></p>

<br>

The Azure Monitor Agent installs automatically when the rule is applied.

<br>
<p align="center">
  <img width="700" height="450" alt="Create data collection rules"
       src="https://github.com/user-attachments/assets/6c722ebd-31ac-47c6-a926-a158cb76205d">
</p>
<p align="center"><em>Figure: Data Collection Rules (DCR)</em></p>


## Verify Log Ingestion

After 5-10 minutes, test log flow in Sentinel. 

**Portal:** Sentinel > Logs

```kql
SecurityEvent
| take 10
```

<p align="center">
  <img width="700" height="450" alt="Security Logs"
       src="https://github.com/user-attachments/assets/358b5a80-89f2-406a-ba57-62ed01952ee0">
</p>
<p align="center"><em>Figure: Security Logs</em></p>

<br>

```kql
SecurityEvent
| where Channel=="Microsoft-Windows-Sysmon/Operational"
```
<p align="center">
  <img width="700" height="450" alt="Sysmon Logs"
       src="https://github.com/user-attachments/assets/a52c45f1-4e23-40f5-bbbf-20d6184292b3">
</p>
<p align="center"><em>Figure: Sysmon Logs</em></p>

<br>

Setup complete. The VM is now sending logs to Sentinel. 

🔗 **Reference Links:**
- https://www.techielass.com/azure-arc-windows-server-setup/
- https://jeffreyappel.nl/deploy-sysmon-and-collect-data-with-sentinel-and-the-ama-agent/
