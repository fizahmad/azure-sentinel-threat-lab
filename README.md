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
- **KQL (Kusto Query Language)** – for detection logic
- **Attack Simulation**
  - Kali Linux (for attacker simulations)
- **Markdown** – for structured write-ups and reporting


## Repository Structure

```
azure-sentinel-threat-lab/
├── README.md                         # Main project overview and roadmap
├── setup/                            # Initial lab setup phase
│   ├── README.md                     # Intro and lab goals for the setup phase
│   ├── azure_account_setup.md       # Guide to creating Azure free trial account
│   ├── kali_vm_setup.md             # Steps for deploying Kali Linux VM (for attack simulation)
│   ├── sentinel_windows_onboarding.md # Connecting Windows VM logs to Sentinel
│   └── windows_vm_setup.md          # Creating and configuring Windows 10 VM via Azure
├── attack-simulation/               # (To be added) Simulated attacks and emulation scripts
├── detections/                      # (To be added) Custom KQL rules for threat detection
├── automation/                      # (To be added) Logic Apps for alert automation
└── reports/                         # (To be added) Detection screenshots and incident writeups
```

## Current Progress

The full lab environment setup is complete. Logs from a Windows 10 Pro VM (onboarded via Azure Arc) are successfully flowing into Microsoft Sentinel. Data connectors and DCRs are active for Security, System, and Application logs.

### Phase 1: Setup Completed
- [x] Azure account with trial credits
- [x] Kali Linux VM deployed and configured
- [x] Azure Arc agent installed on local VM
- [x] Log ingestion via custom Data Collection Rule
- [x] Microsoft Sentinel enabled and connected

> View full setup documentation: [`/setup/`](./setup)


## Next Phase: Simulated Attacks + Detection

Now that the foundational environment is live, the next phase will include:

- Simulating attacks (e.g., credential access, lateral movement, script execution)
- Writing **KQL rules** to detect suspicious behavior
- Building **Logic Apps** to automate alert triage and response

Details will be added in the [`/attack-simulation`](./attack-simulation) and [`/detections`](./detections) folders as progress continues.


## Project Purpose and Motivation

I'm currently learning more about cloud security and blue team roles. I created this lab to apply what I'm studying in a practical way, using Microsoft tools like Azure, Sentinel, KQL, and Logic Apps. Sharing this publicly helps me stay accountable and maybe help others learning too.

## License

This project is released under the [MIT License](LICENSE). Contributions, forks, and feedback are