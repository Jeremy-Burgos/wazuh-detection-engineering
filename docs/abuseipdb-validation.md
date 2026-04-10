# AbuseIPDB Validation

This repository treats AbuseIPDB as a manager-side enrichment workflow.

The goal is to prove that:

- the source SSH rules trigger correctly
- the integration block is configured correctly
- the custom integration runs
- the returned AbuseIPDB fields are present in the alert
- the follow-on rules raise enriched alerts

## Validation model

A clean validation flow looks like this:

1. confirm the custom integration block exists in `ossec.conf`
2. confirm the trigger rule IDs match the integration block
3. confirm the custom integration script is present and executable on the manager
4. add a temporary test log source on a Linux agent
5. inject a failed and successful SSH authentication event from public IP addresses
6. confirm the manager receives the AbuseIPDB enrichment event
7. confirm the follow-on rules fire when the returned abuse confidence score is not zero

## What success looks like

Success means:

- the source event includes a public `srcip`
- the AbuseIPDB integration runs for the configured source rules
- the enriched event contains `abuseipdb.source.rule`
- the enriched event contains `abuseipdb.abuse_confidence_score`
- the public-facing follow-on rule fires cleanly