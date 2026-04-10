# SECURITY

## Scope

This repository contains detection content, supporting configuration examples, and documentation.

It does not ship production deployment automation. It should still be treated carefully because poor rule logic, poor list handling, or unsafe operational assumptions can create real security and operational issues.

## Reporting a security issue

Do not open public issues for:

- secrets accidentally committed
- private infrastructure leakage
- unredacted screenshots or sample data
- unsafe active-response guidance
- content that could create material risk if copied as-is
- malicious contribution attempts

Report security issues privately.

Use GitHub’s private security reporting flow if enabled for the repository. If it is not enabled, contact me through the private security contact method listed on my GitHub profile or website.

## What to include

Please include:

- a clear description of the issue
- the affected file or path
- the potential impact
- exact reproduction steps if reproducible
- whether the issue is disclosure-related, operational, or content-safety-related

## What not to include publicly

Do not post:

- API keys
- webhook URLs
- internal IPs
- production hostnames
- private sample alerts containing sensitive data
- customer names
- copied raw configs with secrets intact

## Response expectations

I review security reports selectively and carefully. Not every report will be resolved on the same timeline, but credible reports will be reviewed.

## Safe use notice

Nothing in this repository should be deployed blindly into production. Validate first. Tune second. Roll back quickly if needed.