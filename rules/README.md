# Rules

This directory contains the custom detection logic for the repository.

The structure is intentionally split by platform so each pack has a clear home and a clear purpose.

## Layout

- `macos/` contains macOS-focused detection content
- `linux/` contains Linux-focused detection content

## Design goals

Rules in this repository should be:

- readable
- scoped to a specific use case
- easy to validate
- safe to roll back
- separated into small packs instead of one giant local rules file

## Rule ID discipline

Keep rule IDs unique.

Do not reuse IDs across files. Do not duplicate IDs from backup or broken files. If you add new content, use a clean numeric range and keep it consistent inside the pack.

A practical pattern is:

- one logical file
- one tight rule range
- one documented purpose

## Rule file expectations

Each rule file should:

- use a clear group name
- use useful descriptions
- avoid vague alert text
- include MITRE mappings where they are genuinely helpful
- avoid mixing unrelated detections into the same file

## Baseline versus example packs

This repository separates baseline packs from threat-specific examples.

Baseline packs are reusable detection building blocks, such as:

- persistence-oriented FIM coverage
- USB monitoring
- AppArmor-related monitoring
- endpoint-focused visibility rules

Threat-specific example packs are narrower and should stay clearly labeled as examples.

## Validation

Do not deploy a new rules file blindly.

Recommended flow:

1. place the file in `/var/ossec/etc/rules`
2. confirm any referenced CDB list is loaded in the Wazuh `<ruleset>` section
3. validate with manager-side checks
4. test with `wazuh-logtest` if the rule is log-driven
5. restart deliberately
6. confirm expected behavior
7. tune or roll back if needed

## What does not belong here

Do not publish:

- `.bak` files
- `.save` files
- abandoned scratch rules
- giant copied rule dumps
- files that still expose private environment details