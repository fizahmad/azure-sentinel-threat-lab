# Setup – Azure Sentinel Threat Detection Lab

This section lays the foundation of the **Azure Sentinel Threat Detection Lab**, designed to simulate real-world SOC operations using cloud-native tools. The primary goal is to build an end-to-end environment where Windows and Linux machines send logs to Microsoft Sentinel for threat detection, investigation, and automated response.

## Lab Infrastructure Overview

To simulate and detect attacks in a cloud-native environment, we set up the following components:

- **Windows VM** – Acts as the primary victim machine. Hosted locally (VirtualBox).
- **Kali Linux VM** – Used to simulate red team attacks. Also hosted locally.
- **Microsoft Sentinel** – Core SIEM system, deployed in Azure.
- **Azure Arc** – Connects the on-prem (local) VMs to Azure for monitoring.
- **Log Analytics Workspace** – Collects logs from connected machines.
- **Data Collection Rules (DCR)** – Define what logs are collected and how they are routed to Sentinel.
- **Logic Apps** *(later)* – Will be used for automated incident response.

---

## Step-by-Step Setup

Each component of the setup process is broken down into dedicated markdown files. Follow them in order:

### 1️⃣ [Prepare the Windows VM](./windows_vm_setup.md)

- Set up a Windows 10 Pro VM in VirtualBox.
- Configure basic settings, install Sysmon, and enable advanced Windows event logging.

### 2️⃣ [Connect Windows VM to Azure using Azure Arc](./sentinel_windows_onboarding.md)

- Use Azure Arc to onboard the local VM as an **Arc-enabled server**.
- This allows remote management and telemetry from Azure.

### 3️⃣ [Prepare and Connect Kali Linux VM](./kali_vm_setup.md)

- Build a Kali Linux VM for later attack simulation.
- Ensure network connectivity with the Windows VM.

### 4️⃣ [Configure Azure Account & Sentinel Workspace](./azure_account_setup.md)

- Set up an Azure account and create a **Log Analytics Workspace**.
- Deploy **Microsoft Sentinel** on top of it.
- Create necessary resource groups, automation accounts, and permissions.

---

## Outcome

✅ Windows VM is sending logs (Security, System, Application, Sysmon, etc.) to Microsoft Sentinel  
✅ Kali Linux VM will be ready for executing attack scenarios  
✅ Microsoft Sentinel will be fully integrated with the Log Analytics Workspace and ready to receive and detect events  

> All screenshots are stored inside [`/setup/screenshots`](./screenshots/)