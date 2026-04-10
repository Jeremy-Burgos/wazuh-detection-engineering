# AbuseIPDB Integration Notes

This repository includes a manager-side AbuseIPDB integration workflow for SSH authentication events from public IP addresses.

## What this workflow does

The AbuseIPDB integration enriches selected SSH authentication alerts with reputation data returned by the AbuseIPDB API.

The workflow is:

1. a source rule detects an SSH authentication event from a public IP address
2. the custom `custom-abuseipdb.py` integration runs
3. the integration checks the source IP against AbuseIPDB
4. follow-on rules evaluate the returned abuse confidence score
5. the enriched event raises a clearer alert

## Why this is separate from CDB IP reputation

This is not the same as a static CDB list lookup.

A CDB list is a local static dataset.
AbuseIPDB is a dynamic external API lookup.

Both are useful, but they solve different problems and should stay separate in the repository.

## What belongs in the repository

This repository includes:

- source rules for public-IP SSH authentication attempts
- follow-on rules for AbuseIPDB enrichment
- documentation for validation
- manager integration examples