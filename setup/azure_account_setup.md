# Azure Account Setup

From here, key services for our lab setup include:

| Service | Description |
|--------|-------------|
| **Azure Arc** | For onboarding non-Azure Windows/Linux machines |
| **Log Analytics Workspace** | Used to ingest logs |
| **Microsoft Sentinel** | SIEM layer activated on top of the workspace |
| **Resource Groups** | Logical containers to manage resources in the lab |

## Free Trial

Azure offers a free trial with $200 credit for 30 days - sufficient for this lab.

**Sign up:** https://azure.microsoft.com/en-us/free/

After signing in, the portal looks like this:

<p align="center">
  <img width="700" height="450" alt="Azure Dashboard"
       src="https://github.com/user-attachments/assets/3efdfcb6-277f-4088-9cec-6b61a2da788d">
</p>

<p align="center"><em>Figure: Azure Dashboard</em></p>

## Resource Group

Created a resource group to organize all lab resources. 

**Portal:** Resource groups > Create

| Setting | Value |
|---------|-------|
| Name | `sentinel-lab-rg` |
| Region | East US |

<p align="center">
  <img width="700" height="450" alt="Resource Group"
       src="https://github.com/user-attachments/assets/ae9911a7-d888-49f2-b63e-e71ebe946dfe">
</p>

<p align="center"><em>Figure: Resource Group</em></p>

## Log Analytics Workspace

The workspace stores all collected logs.  Sentinel reads from this.

**Portal:** Log Analytics workspaces > Create

| Setting | Value |
|---------|-------|
| Resource Group | `sentinel-lab-rg` |
| Name | `sentinel-lab-law` |
| Region | East US |

<p align="center">
  <img width="700" height="450" alt="Log Analytics workspace"
       src="https://github.com/user-attachments/assets/8544744a-920f-4a7e-bec4-9fbc28d3484f">
</p>

<p align="center"><em>Figure: Log Analytics workspace</em></p>

## Enable Microsoft Sentinel

Added Sentinel to the workspace. 

**Portal:** Microsoft Sentinel > Create > Select workspace > Add

<p align="center">
  <img width="700" height="450" alt="Sentinel"
       src="https://github.com/user-attachments/assets/b9897e5c-9bd3-4c52-9cc1-4dd7625f16ff">
</p>

<p align="center"><em>Figure: Sentinel Added to Workspace</em></p>


Next:  [Windows VM Setup](./windows_vm_setup.md)
