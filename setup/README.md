# ⚙️ Lab Setup Overview

This folder contains detailed documentation for setting up the core infrastructure of this SOC lab simulation.

## Purpose:

To build a local + cloud hybrid SOC lab environment that includes a **victim (Windows 10)** machine, an **attacker (Kali Linux)** machine, and integration with **Azure Sentinel** for detection and automation.



## 🧱 Setup Components:

| Component              | Purpose                          | File                                  |
|------------------------|----------------------------------|---------------------------------------|
| Azure Free Account     | Cloud backend + Sentinel SIEM    | [azure_account_setup.md](./azure_account_setup.md) |
| Windows 10 Pro VM      | Target of attacks (victim)       | [windows_vm_setup.md](./windows_vm_setup.md)       |
| Kali Linux VM          | Simulate attacks (attacker)      | [kali_vm_setup.md](./kali_vm_setup.md)             |


