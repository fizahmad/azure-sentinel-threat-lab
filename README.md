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
- Setup guides complete
- 21 Sentinel analytic rules built (001–021)
- Attack simulation mappings documented
- Automation playbook templates added
- Reports structure defined

## How to Use This Lab

1. **Setup** → Follow `setup/README.md` to build the Azure + VM environment.
2. **Detections** → Import YAMLs from `detections/` into Sentinel as Scheduled analytic rules.
3. **Simulate** → Use `attack-simulation/README.md` commands (lab-only) to trigger detections.
4. **Automate** → Deploy Logic Apps from `automation/` for incident response.
5. **Document** → Capture findings in `reports/` per the template structure.

## Detection Coverage

21 analytic rules spanning MITRE ATT&CK tactics:
- **Execution** (5 rules) — PowerShell abuse, Office macros, LOLBins
- **Credential Access** (5 rules) — LSASS dumps, SAM copy, RDP brute-force, DCSync
- **Lateral Movement** (5 rules) — SMB, PsExec, WMI, WinRM
- **Persistence** (4 rules) — Scheduled tasks, registry Run keys, WMI subscriptions, new admin accounts
- **Defense Evasion** (2 rules) — AMSI bypass, Defender tampering
- **Impact** (1 rule) — Shadow copy deletion

Each rule includes severity, MITRE mapping, query frequency, and data connector requirements.

## Project Purpose and Motivation

I'm currently learning more about cloud security and blue team roles. I created this lab to apply what I'm studying in a practical way, using Microsoft tools like Azure, Sentinel, KQL, and Logic Apps. 

Sharing this publicly helps me stay accountable and maybe help others learning too.
