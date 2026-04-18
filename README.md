# Threat Detection Lab using Microsoft Sentinel 

This project replicates a Security Operations Center (SOC) workflow using **Microsoft Sentinel** in **Azure**. 

## Objectives

- Deploy a lab environment on Azure
- Onboard Windows systems via Azure Arc
- Simulate adversary behavior using known TTPs
- Build custom **KQL detection rules**
- Automate alerts with **Logic Apps**
- Validate detections in Sentinel and document findings

## Tools & Technologies

- **Microsoft Azure**
  - Azure Arc (for onboarding non-Azure machines)
  - Log Analytics Workspace (centralized log collection)
  - Microsoft Sentinel (SIEM)
  - Logic Apps (SOAR automation)
- **KQL (Kusto Query Language)**
  - for detection logic
- **Attack Simulation**
  - Windows VM (Security logs + optional Sysmon)
  - Linux VM (optional)
- **Markdown**
  - for documentation 

## Repository Structure

```
azure-sentinel-threat-lab/
├── README.md                              # Main project overview
├── setup/                                 # Initial lab setup phase
├── parsers/                               # Optional KQL parsers / normalization helpers
├── detections/                            # Custom KQL rules for threat detection
├── attack-simulation/                     # Simulated attacks and emulation steps (lab-only)
├── automation/                            # Logic Apps playbooks for alert automation
└── reports/                               # Detection screenshots and incident writeups
```

## How to Use This Lab

1. **Setup** → Follow `setup/` to build the Azure + VM environment. 
2. **Parsers** → Deploy functions from `parsers/` if you are using them.
3. **Detections** → Import rules from `detections/` into Sentinel analytics.
4. **Simulate** → Use `attack-simulation/` steps to trigger detections (lab-only).
5. **Automate** → Deploy Logic Apps from `automation/` for incident response.
6. **Document** → Capture findings in `reports/`.

## Notes

- This repo is for learning and lab testing only.
- Do not run attack simulations on production systems.