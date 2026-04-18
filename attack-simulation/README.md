# Attack Simulation Guide

Purpose: Provide reproducible behaviors for each detection rule. Run only in this lab; do not execute on production assets.

## Prereqs
- Windows target VM with log ingestion working per `setup/`.
- Security logw are recommended baseline.
- Sysmon is optional (adds richer telemetry).
- PowerShell run as Administrator; enable local script execution if needed.

## How to use
- Each file in this folder maps to a detection rule.
- Run the commands/steps on the lab VM.
- Then validate in Sentinel:
  - Confirm logs arrived
  - Confirm the analytic rule matches
  - Confirm an incident is created (if enabled)
- Add screenshots and notes to `reports/`.

## Notes
- Prefer safe/controlled commands in a lab environment.
- Clean up artifacts after testing (tools, dumps, tasks, test accounts).