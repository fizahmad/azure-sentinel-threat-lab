# 🤖 Alert Automation (Logic Apps)

This folder contains exported workflows from Azure Logic Apps that automate incident response actions.

## Included (examples)
- `playbook-alert-to-email.json` — On Sentinel incident creation: get incident → extract entities → send email to SOC DL.
- `playbook-alert-to-teams.json` — Post to Teams webhook with incident link and entities.
- `playbook-auto-contain-host.json` — (placeholder) Isolate host via Defender for Endpoint API when high-severity alert fires.

## How to import
1) Sentinel > Automation > Create > Import playbook (Logic App) > Upload JSON.
2) Fix connections: `azureloganalytics`, `office365`, `teams` as prompted.
3) Grant the Logic App `Microsoft Sentinel Responder` role to the workspace.
4) Enable the playbook as an automation rule (Incident triggers: `When Azure Sentinel incident is created`).

## Suggested automation rules
- Severity >= High → Run `playbook-auto-contain-host.json` (after you create a service principal with isolate permissions).
- All severities → Run `playbook-alert-to-email.json` for awareness.
- Lateral movement detections → Run `playbook-alert-to-teams.json` to SOC channel.

## Notes
- Keep one playbook per action; chain via automation rules to stay modular.
- Store any secrets (webhook URLs, SP credentials) in Key Vault and reference via managed identity.
- Sample payload mappings are annotated inside each JSON file.
