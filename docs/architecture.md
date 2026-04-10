# Architecture

This repository is built around a simple idea:

keep the public content modular, grounded, and safe to reason about.

It reflects a real Wazuh deployment, but the repository itself is not a mirror of the live environment. It is a sanitized, publication-ready structure designed to preserve the useful engineering while removing private details and operational noise.

## Baseline deployment model

The source environment behind this repository is a single all-in-one Wazuh deployment.

That means:

- Wazuh manager, indexer, and dashboard run on one Ubuntu host
- custom rules live under `/var/ossec/etc/rules`
- custom decoders live under `/var/ossec/etc/decoders`
- list-backed logic depends on CDB lists declared in the Wazuh `<ruleset>` section
- the repository is documented as a single-node baseline, not a cluster guide

## Repository design model

The repository is split by function, not by convenience.

### `rules/`

This directory holds the detection logic.

It is divided by platform so readers can quickly understand what applies to Linux, what applies to macOS, and what is intended as a threat-specific example versus a baseline detection pack.

Examples:

- macOS persistence FIM
- macOS USB monitoring
- macOS endpoint visibility
- Linux AppArmor-related monitoring
- Linux persistence techniques
- Linux USB examples
- Linux malware example packs

### `decoders/`

This directory holds custom parsing logic.

The structure is intentionally split into:

- `common/` for reusable decoders
- `macos/` for platform-specific parsing
- `linux/` only where custom parsing is genuinely required

The repository avoids creating custom decoders for sources Wazuh already handles well enough by default.

### `lists/`

This directory holds sanitized IOC or allowlist examples.

The public repository includes example formats, not private live feeds.

The goal is to show:

- how the list is structured
- what the lookup is meant to support
- how list-backed rules should be wired

### `examples/`

This directory is reserved for safe configuration examples.

It should contain small, focused snippets that demonstrate placement and structure without exposing private environment details.

Examples should be redacted, minimal, and purpose-driven.

## Content layers

The repository is intentionally organized into three content layers.

### 1. Baseline packs

These are the main reusable building blocks.

They should be the first content a reader trusts, tests, and tunes.

Examples:

- macOS persistence FIM
- Linux persistence techniques
- Linux AppArmor FIM
- macOS USB device monitoring
- common decoder packs

### 2. Threat-specific examples

These are narrower packs kept clearly separate from the baseline.

They exist to show how a real Wazuh repository can include targeted detection content without turning the whole project into a malware zoo.

Examples:

- FrigidStealer
- Koske

### 3. Example IOC formats

These demonstrate CDB structure and usage patterns without claiming to be authoritative intelligence feeds.

They exist to teach safe structure, not to serve as production-ready threat intelligence by default.

## Operational philosophy

This repository favors:

- manual placement over blind automation
- validation before restart
- rollback before improvisation
- clear scope over inflated coverage
- redaction discipline over screenshots and raw data dumps

## What this architecture avoids

This repository intentionally avoids:

- monolithic `local_rules.xml` sprawl
- catch-all decoder files with unrelated logic mixed together
- backup files, scratch files, or broken files in the public tree
- automation that hides what is being deployed
- documentation that pretends examples are universal

## Validation boundary

The repository content is meant to be validated in stages.

A safe path looks like this:

1. add one rules file or decoder file
2. confirm list registration if needed
3. validate configuration
4. test the event logic
5. restart deliberately
6. observe the result
7. tune or roll back if needed

This architecture assumes that detection content is operational content, not just code.
