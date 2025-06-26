# Azure Sentinel Threat Detection Lab – End-to-End SOC Simulation

This project simulates a real-world Security Operations Center (SOC) workflow using **Microsoft Sentinel** in **Azure**. 

It includes:
- Lab setup using Azure virtual machines and Log Analytics
- Simulated cyberattacks using known TTPs
- Custom **KQL detection rules**
- Automated alerting with **Azure Logic Apps**
- Structured incident documentation

The goal is to showcase hands-on capabilities in **cloud-native threat detection**, **security monitoring**, and **response automation** using Microsoft’s security ecosystem.

## Tools & Technologies

- **Microsoft Azure**
  - Virtual Machines (for attack targets)
  - Log Analytics Workspace (for centralized logging)
  - Microsoft Sentinel (SIEM solution)
  - Logic Apps (for SOAR automation)
- **KQL (Kusto Query Language)** – for writing custom detection rules
- **Attack Simulation Frameworks**
  - Atomic Red Team
  - MITRE CALDERA
- **Markdown** – for structured documentation and reporting

## Contents
```
azure-sentinel-threat-lab/
├── README.md → Project overview & documentation
├── setup/ → Azure deployment & config steps
├── attack-simulation/ → Steps/scripts for simulating attacks
├── detections/ → Custom KQL detection rules
├── automation/ → Logic App workflows (JSON exports)
└── reports/ → Screenshots & incident reports
```

### Lab Setup (See `/setup/` folder)

- Created an Azure trial account
- Deployed a Windows VM as a target system
- Connected logs to Log Analytics
- Enabled Microsoft Sentinel on the workspace
- Configured data connectors (Security Events, Sysmon, etc.)

### Attack Simulation (See `/attack-simulation/`)

Simulated basic attack behaviors to test detection logic, such as:
- PowerShell-based command execution
- Brute force login attempts
- Suspicious script behaviors

### Detection Rules (`/detections/`)

Wrote custom **KQL queries** to catch suspicious activities in logs, such as:
- Encoded PowerShell commands
- Repeated failed logins from the same IP
- Suspicious child process creation

### Alert Automation (`/automation/`)

Used **Azure Logic Apps** to respond to alerts by:
- Sending email notifications
- Triggering simple response flows
- Logging incidents for review

### Notes & Reports (`/reports/`)

Each test scenario includes:
- A short write-up of what was simulated
- Screenshots of detection/alerting
- Notes on what worked or failed

## Current Progress

> This project is in its early stages and is being built step by step as part of my learning journey in cloud-based SOC operations.

### Phase 1: Lab Environment Setup [*In Progress*]
- Setting up Azure VM and workspace
- Connecting VM logs to Log Analytics
- Enabling and configuring Microsoft Sentinel

### Upcoming:
- Simulating real-world TTPs in the lab
- Writing detection rules using KQL
- Automating alert response with Logic Apps

I'll continue to update this repo as I complete each phase.

## Why I Made This

I'm currently learning more about cloud security and blue team roles. I created this lab to apply what I’m studying in a practical way, using Microsoft tools like Sentinel, KQL, and Logic Apps. Sharing this publicly helps me stay accountable and maybe help others learning too.

#### License

This project is open-source and shared under the [MIT License](LICENSE). Anyone is welcome to explore, fork, or learn from it.
