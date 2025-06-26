# 🔎 Detection Rules (KQL)

This folder contains custom detection queries written in KQL (Kusto Query Language) for Microsoft Sentinel.

Each query targets specific behaviors:
- Encoded PowerShell usage
- Excessive failed login attempts
- Rare parent-child process chains
- Suspicious system utility usage (e.g. `whoami`, `net.exe`)

Detection rules are saved as `.kql` files or `.txt` for review and reuse.
