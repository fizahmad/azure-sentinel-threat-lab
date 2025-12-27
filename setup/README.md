# Lab Setup

This lab uses a local Windows VM connected to Microsoft Sentinel via Azure Arc.  All logs are collected and analyzed in the cloud while the VM runs on my machine.

## Components

| Component | Purpose |
|-----------|---------|
| Windows 10 VM | Target machine for attack simulation |
| Azure Arc | Connects local VM to Azure |
| Log Analytics Workspace | Centralized log storage |
| Microsoft Sentinel | SIEM for detection and alerting |
| Sysmon | Enhanced Windows logging |

## Architecture

```
┌──────────────────┐         ┌─────────────────────────────┐
│                  │         │           Azure             │
│ Windows Machine  │────────►│                             │
│                  │  Azure  │  Log Analytics ─► Sentinel  │
│   + Sysmon       │   Arc   │                             │
│   + Arc Agent    │         │                             │
└──────────────────┘         └─────────────────────────────┘
```

## Setup Guides

Complete these in order:

1. **[Azure Account Setup](./azure_account_setup.md)** - Create free Azure account, Log Analytics Workspace, and enable Sentinel

2. **[Windows VM Setup](./windows_vm_setup.md)** - Configure Windows 10 VM with Sysmon and required logging

3. **[Sentinel Onboarding](./sentinel_windows_onboarding.md)** - Connect VM to Azure using Arc and configure data collection
