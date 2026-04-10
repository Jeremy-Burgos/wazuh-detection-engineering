# VirusTotal Validation

This repository treats VirusTotal as a manager-side enrichment workflow for file hashes observed by Wazuh FIM.

## Validation goals

The goal is to prove that:

- FIM detects the file event
- the VirusTotal integration is configured correctly
- the integration receives a file-hash-bearing alert
- the manager queries VirusTotal successfully
- the expected enrichment alert appears

## Validation model

A clean validation flow looks like this:

1. confirm the VirusTotal integration block exists in `ossec.conf`
2. confirm it is scoped to the `syscheck` group
3. confirm a monitored path under FIM is active
4. create or modify a benign test file in the monitored path
5. confirm the FIM alert contains a file hash
6. confirm the VirusTotal integration processes the event
7. review the resulting enrichment alert

## What success looks like

Success means:

- the FIM event occurs
- the integration runs without configuration errors
- the resulting alert clearly reflects the VirusTotal lookup path
- the workflow can be explained and demonstrated without exposing secrets

