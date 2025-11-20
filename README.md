# Threat Detection Lab using Microsoft Sentinel 

This project replicates a Security Operations Center (SOC) workflow using **Microsoft Sentinel** in **Azure**.

## Objectives

- Deploy a lab environment on Azure
- Onboard Windows systems via Azure Arc
- Simulate adversary behavior using known TTPs
- Build custom **KQL detection rules**
- Automate alerts with **Logic Apps**

## Tools & Technologies

- **Microsoft Azure**
  - Azure Arc (for onboarding non-Azure machines)
  - Log Analytics Workspace (centralized log collection)
  - Microsoft Sentinel (SIEM)
  - Logic Apps (SOAR automation)
- **KQL (Kusto Query Language)**
  - for detection logic
- **Attack Simulation**
  - Debian-based Linux (for attack simulations)
- **Markdown**
  - for documentation 


## Repository Structure

```
azure-sentinel-threat-lab/
├── README.md                              # Main project overview and roadmap
├── setup/                                 # Initial lab setup phase
│   ├── README.md                          # Intro and lab goals for the setup phase
│   ├── azure_account_setup.md             # Guide to creating Azure free trial account
│   ├── kali_vm_setup.md                   # Steps for deploying Linux VM (for attack simulation)
│   ├── sentinel_windows_onboarding.md     # Connecting Windows VM logs to Sentinel
│   └── windows_vm_setup.md                # Creating and configuring Windows 10 VM via Azure
├── attack-simulation/                     # Simulated attacks and emulation scripts
├── detections/                            # Custom KQL rules for threat detection
├── automation/                            # Logic Apps for alert automation
└── reports/                               # Detection screenshots and incident writeups
```

**Status** 
- In Progress


## Project Purpose and Motivation

I'm currently learning more about cloud security and blue team roles. I created this lab to apply what I'm studying in a practical way, using Microsoft tools like Azure, Sentinel, KQL, and Logic Apps. 

Sharing this publicly helps me stay accountable and maybe help others learning too.
