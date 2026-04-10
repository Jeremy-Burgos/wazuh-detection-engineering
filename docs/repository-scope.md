# Repository Scope

This repository is intentionally curated.

The goal is not to publish every file that ever existed in the source environment. The goal is to publish the parts that are technically useful, structurally clean, and safe to share.

## What this repository is

This repository is:

- a public Wazuh detection-engineering repository
- based on a real deployment
- sanitized for publication
- organized for clarity, validation, and reuse
- written for defenders, researchers, and technical reviewers

## What this repository is not

This repository is not:

- a full Wazuh installation guide
- a production automation bundle
- a cluster operations guide
- a generic malware-rule archive
- a place for unreviewed bulk rule dumps
- a mirror of all private lab content

## In scope

The following are in scope:

### Rules

Custom rules that are:

- meaningful
- readable
- scoped to a clear use case
- safe to validate incrementally
- organized by platform or purpose

### Decoders

Custom decoders that are:

- necessary for the target log source
- clearly named
- separated by purpose
- validated against realistic sample data

### IOC and allowlist examples

Public example files that show:

- correct CDB formatting
- realistic lookup use cases
- clean separation between examples and live intelligence

### Documentation

Documentation that explains:

- architecture
- validation
- rollback
- redaction
- contribution expectations
- security reporting
- environment assumptions
- operational limits

### Threat-specific examples

A small number of clearly separated threat-specific packs that strengthen the repository without overwhelming it.

## Out of scope

The following are out of scope unless explicitly added later:

- private indicators from real investigations
- unredacted screenshots
- infrastructure-specific hostnames or URLs
- internal IP space
- raw secrets or webhook details
- experimental scratch content
- broken files
- bulk imports from third-party repositories
- content that was never validated even at a basic level

## Rules for inclusion

A file should be included only if it meets at least these standards:

1. it has a clear purpose
2. it belongs in the final public structure
3. it is not a backup or recovery artifact
4. it does not expose sensitive data
5. it is understandable without private context
6. it supports the repository’s actual editorial spine

## Editorial spine

This repository is strongest when it stays centered on:

- Linux and macOS detection content
- persistence
- endpoint visibility
- USB monitoring
- AppArmor and FIM-related detections
- selected list-backed logic
- a small number of threat-specific examples

That is the core.

Anything outside that should justify its place.

## Quality bar

Content in this repository should aim to be:

- direct
- technically credible
- easy to reason about
- honest about limitations
- safe to validate
- structured for maintenance
