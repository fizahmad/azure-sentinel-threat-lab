# 📄 Reports & Findings

This folder holds incident writeups, screenshots, and observations from lab runs.

## Includes
- Step-by-step incident reports
- Sentinel alert screenshots
- Notes on detection logic performance
- Observations on gaps, false positives, and improvement areas

## Suggested structure
- `incidents/` — One markdown per incident: context, timeline, evidence (KQL results), remediation.
- `screenshots/` — Alert, entity, and investigation graph captures.
- `metrics.md` — Detection hit counts, false positives, tuning notes.

## What to capture per incident
- Triggering detection name + MITRE technique.
- Host/user/resource involved; UTC timestamps.
- KQL snippets used for triage/hunting.
- Impact + recommended response (containment, eradication, recovery).
- Tuning applied (suppression, allowlists, scope adjustments).

## Tips
- Redact real names/IPs if sharing publicly.
- Date-prefix files for ordering, e.g., `2025-12-10-lsass-dump.md`.
- Link back to the detection YAML and the attack-simulation step used.
