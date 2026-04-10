# VirusTotal Integration Notes

This repository includes VirusTotal as a manager-side FIM hash enrichment workflow.

## How the workflow works

The workflow is:

1. Wazuh FIM detects a new or modified file
2. the VirusTotal integration extracts the file hash from the FIM alert
3. the manager queries VirusTotal with that hash
4. Wazuh raises integration-driven alerts based on the returned result
5. optional follow-on response logic can act on a high-confidence malicious result

## Why this repository keeps VirusTotal lightweight

The current repository already covers:

- FIM
- shared malware-hash CDB matching
- YARA active-response scanning
- removal-oriented response notes

So VirusTotal fits best here as a documented integration and validation path, not as another large custom rule family.

## Repository components for VirusTotal

This repository uses:

- `examples/manager/ossec.conf.integrations.example.xml`
- `docs/virustotal-integration-notes.md`
- `docs/virustotal-validation.md`

