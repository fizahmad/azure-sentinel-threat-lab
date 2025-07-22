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