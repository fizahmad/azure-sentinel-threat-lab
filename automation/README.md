# Alert Automation (Logic Apps)

This folder contains Logic Apps playbooks used to automate incident response in Microsoft Sentinel.

## Examples of automation
- Notify (Email / Teams)
- Enrich (add entities, lookups, tagging)
- Respond (contain host, disable user) — lab-only and permission-dependent

## How to import
1) Sentinel → Automation → Create → Import playbook (Logic App) → Upload JSON  
2) Fix connections as prompted  
3) Assign required roles to the Logic App identity  
4) Enable via Automation Rules (trigger on incident creation)

## Notes
- Keep playbooks modular (one action per playbook where possible).
- Store secrets in Key Vault and reference via managed identity.