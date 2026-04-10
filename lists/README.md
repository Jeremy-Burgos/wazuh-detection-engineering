# Lists

This directory contains sanitized IOC and allowlist examples for CDB-backed workflows.

The public repository should demonstrate structure and usage, not publish private lab intelligence feeds or internal allowlists.

## Layout

- `ioc/` contains example files for:
  - malicious IPs
  - malicious domains
  - malware hashes
  - suspicious programs
  - USB device allowlists

## Repository policy

Files in this repository are examples unless explicitly documented otherwise.

That means:

- they demonstrate format
- they demonstrate lookup intent
- they should not be treated as production threat intelligence by default

## CDB usage model

Wazuh CDB-backed logic depends on two things:

1. the list must be registered in the Wazuh `<ruleset>` section
2. the rule must reference the list using a `<list ...>...</list>` lookup

A list file that exists on disk but is never registered or referenced does nothing.

## Common use cases

This repository uses lists for:

- malware hash matching
- suspicious program lookup
- USB allowlist checks
- IP reputation style lookups
- keyed metadata matching for audit-related logic

## Formatting expectations

Keep list formats simple and deliberate.

Typical examples include:

- `key:value`
- `key:label`
- `hash:family`
- `serial:approved_device`

Do not overload list files with inconsistent structures.

## Public-safe examples

Public example files should:

- use safe placeholder values
- avoid private investigation data
- avoid live customer or lab identifiers
- preserve realistic shape and usage

## What does not belong here

Do not publish:

- private IOC feeds
- private allowlists
- internal device identifiers
- raw exports from active investigations
- stale or unexplained list files with no documented purpose