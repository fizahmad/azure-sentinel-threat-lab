# Detections

This folder contains detection rules meant to be imported into **Microsoft Sentinel** analytics.

## What’s inside
- One YAML file per detection rule
- KQL query logic + rule metadata (severity, tactics/techniques, scheduling)

## How to use
1. Microsoft Sentinel → Analytics → Create rule (Scheduled or NRT where appropriate)
2. Copy the query + settings from the YAML file
3. Enable incident creation
4. Use `attack-simulation/` to trigger the behavior
5. Document results in `reports/`

## Notes
- Field names can vary depending on your connector (SecurityEvent, Sysmon, MDE, etc.).
- Tune queries to reduce false positives based on your lab telemetry.