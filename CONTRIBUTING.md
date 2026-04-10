# CONTRIBUTING

Thanks for taking the time to review or contribute to this repository.

This repository is intentionally curated. I care more about clarity, correctness, and operational safety than volume.

## Before opening an issue or pull request

Read these first:

- `README.md`
- `TESTED_ON.md`
- `SECURITY.md`

If the topic is security-sensitive, use the private reporting path in `SECURITY.md` instead of a public issue.

## What is welcome

Useful contributions include:

- bug reports with reproducible details
- false-positive reports with clear event context
- careful corrections to rules, decoders, or documentation
- narrowly scoped detection-content submissions with sample log format and validation notes
- documentation fixes that improve accuracy or safety

## What is not helpful

Do not submit:

- giant rule dumps with no validation notes
- copied third-party content with minimal changes
- vague “add more malware rules” requests
- unredacted configs
- environment-specific content presented as generic
- changes that increase complexity without improving quality

## Content standards

Any rules or decoders proposed here should:

- use clear naming
- avoid duplicate IDs
- avoid duplicate decoder names
- include a clear description
- document assumptions where needed
- note likely false-positive conditions when relevant
- be validated before being proposed for merge

## IOC and CDB list standards

List examples should be:

- sanitized
- clearly labeled as examples when not sourced from a maintained feed
- formatted correctly for Wazuh CDB use
- tied to a believable use case

## Pull request expectations

Pull requests should be small, focused, and readable.

Include:

- what changed
- why it changed
- how it was validated
- whether it changes behavior, coverage, or only documentation
- any rollback or tuning considerations

## Merge policy

Opening a pull request does not guarantee merge.

This repository is selectively maintained. Contributions may be accepted, revised, deferred, or declined.

## Redaction

Never submit:

- secrets
- keys
- private IPs
- internal hostnames
- customer data
- sensitive screenshots
- raw logs that should not be public