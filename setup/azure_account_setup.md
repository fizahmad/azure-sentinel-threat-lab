# Azure Account Setup

## Free Trial

Azure offers a free trial with $200 credit for 30 days - sufficient for this lab.

**Sign up:** https://azure.microsoft.com/en-us/free/

After signing in, the portal looks like this:

<img width="700" height="450" alt="2025-12-27_20-29" align="center" src="https://github.com/user-attachments/assets/3efdfcb6-277f-4088-9cec-6b61a2da788d" />
<p align="center"> Figure: Azure Dashboard </p>                                              

## Resource Group

Created a resource group to organize all lab resources. 

**Portal:** Resource groups > Create

| Setting | Value |
|---------|-------|
| Name | `sentinel-lab-rg` |
| Region | East US |

<img width="700" height="450" alt="2025-12-27_20-33" src="https://github.com/user-attachments/assets/ae9911a7-d888-49f2-b63e-e71ebe946dfe" />
<p align="center"> Figure: Resource Group </p>                                              

## Log Analytics Workspace

The workspace stores all collected logs.  Sentinel reads from this.

**Portal:** Log Analytics workspaces > Create

| Setting | Value |
|---------|-------|
| Resource Group | `sentinel-lab-rg` |
| Name | `sentinel-lab-law` |
| Region | East US |

![Log Analytics Workspace](./log_analytics_workspace. png)

## Enable Microsoft Sentinel

Added Sentinel to the workspace. 

**Portal:** Microsoft Sentinel > Create > Select workspace > Add

![Sentinel Enabled](./sentinel_enabled.png)

Azure setup complete. Next:  [Windows VM Setup](./windows_vm_setup.md)





------------------
# Azure Account Setup – Microsoft Sentinel Lab

## Objective

To set up an Azure environment for Microsoft Sentinel by:
- Creating a new Azure account with a **free trial**
- Setting up core services required for Sentinel log ingestion
- Preparing for onboarding non-Azure machines (via Azure Arc)

## Free Trial Subscription

In order to get a Azure **Free Trial** that includes:
- $200 USD credit for 30 days
- Access to all core Azure services
- No charges unless you upgrade manually

🔗 [Create a Free Azure Account](https://azure.microsoft.com/en-us/free/)

## After Signing Up

Once your Azure account is ready and you're signed into the portal, you'll land on the **Azure Home Dashboard**.

Ref: [azure_dashboard.png](./screenshots/azure_dashboard.png)

From here, key services for our lab setup include:

| Service | Description |
|--------|-------------|
| **Azure Arc** | For onboarding non-Azure Windows/Linux machines |
| **Log Analytics Workspace** | Used to ingest logs |
| **Microsoft Sentinel** | SIEM layer activated on top of the workspace |
| **Resource Groups** | Logical containers to manage resources in the lab |

Ref: [resource_group_created.png](./screenshots/resource_group_created.png)
