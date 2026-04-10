# WordPress SCA Notes

This repository includes a WordPress security assessment example built with the Wazuh Security Configuration Assessment module.

## Why this belongs in the repository

The rest of this repository is focused on detections, decoders, CDB-backed logic, integrations, and validation.

This WordPress pack adds a different capability:
application hardening assessment.

That makes the repository stronger because it shows Wazuh being used not only for alerting and enrichment, but also for configuration and exposure review on a real application stack.

## Scope

This example is intended for:

- Linux endpoints
- self-hosted WordPress on a dedicated private server
- environments where `wp-cli` is installed on the endpoint

This is not intended for shared hosting where the server-level checks or path assumptions do not apply cleanly.

## What the example checks

The example policy checks:

- WordPress core currency
- debug mode exposure
- common administrative usernames
- backup or database dump files in the web root
- file permissions
- directory permissions
- `.htaccess` permissions
- directory browsing
- default database prefix usage
- presence of a security or firewall plugin