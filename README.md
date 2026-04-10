# Wazuh Detection Engineering

Sanitized Wazuh detection content built from a real Ubuntu-based deployment.

This repository focuses on practical custom rules, custom decoders, IOC list design, active validation, and operator-safe implementation guidance. It is meant to be useful to defenders running modern Wazuh, and readable to engineers or business owners reviewing my work.

## Scope

This repository includes:

- Custom Wazuh rules for Linux and macOS
- Custom decoders for selected log sources
- Example IOC and allowlist CDB list formats
- Threat-specific example content that is clearly separated from the baseline packs
- Documentation written around manual placement, validation, rollback, and redaction discipline

This repository does not include:

- Turnkey production deployment automation
- Full infrastructure provisioning
- Blind copy-all scripts
- Unredacted live environment data
- Claims that every example here is universally safe to deploy without tuning

## Why this repository exists

A lot of public Wazuh content is either too generic, too noisy, or too tied to one narrow setup. The goal here is different:

- keep the structure clean
- keep the scope honest
- keep the content reusable
- document real operational tradeoffs
- make validation and rollback first-class parts of the workflow

## Who this is for

This repository is aimed at:

- Wazuh practitioners
- home lab users
- security researchers
- SOC analysts
- Linux defenders
- blue team engineers
- business owners looking at my GitHub profile

## Baseline environment

The content in this repository was shaped against a real all-in-one Wazuh deployment with custom rules, decoders, and CDB lists, running on Ubuntu 24.04.4 with Wazuh 4.14.4 components. Cluster settings existed in the live configuration but were disabled, so this repository is documented as a single-node baseline, not a cluster guide.

For exact version and environment notes, see [TESTED_ON.md](TESTED_ON.md).

## Repository layout

```text
rules/
  macos/
  linux/
  shared/

decoders/
  shared/
  macos/
  linux/

lists/
  ioc/

examples/
  manager/
  agent/
````

## Content design

The repository is intentionally split into:

1. Baseline packs
   These are practical detection building blocks such as macOS persistence FIM, macOS USB monitoring, Linux AppArmor FIM, Linux persistence coverage, and common decoders.

2. Threat-specific examples
   These are narrower packs, such as FrigidStealer or Koske, kept clearly separate so they do not blur the baseline content.

3. Example IOC formats
   The `.example` files under `lists/ioc/` are sanitized examples for structure and workflow. They are not intended to be treated as authoritative threat intelligence feeds.

## Installation philosophy

This repository assumes manual copy and placement.

That is deliberate.

Security content should be reviewed before it is deployed. Rules, decoders, and list-backed logic can create noise, false positives, unexpected alert volume, or active response consequences if dropped into the wrong environment without validation.

Review the content first. Back up your current configuration. Add one pack at a time. Validate. Restart deliberately. Roll back quickly if needed.

## Validation workflow

Recommended order:

1. Add or update one rules file or decoder file
2. Confirm any referenced list is registered in the Wazuh `<ruleset>` section
3. Validate configuration and parsing
4. Restart the manager only after validation succeeds
5. Confirm expected alerts with controlled test data
6. Record any tuning or false positives before expanding further

Use Wazuh’s config and test tooling as part of every change, not just after breakage.

## Risks and guardrails

This repository assumes you understand the following risks:

* duplicate rule IDs can break or distort detections
* duplicate decoder names create confusion
* broad FIM paths can create heavy noise
* IOC lists are only useful if they are actually wired to active rules
* active response can create real operational impact
* copied examples often need environment-specific tuning

## Redaction policy

Nothing in this repository should expose:

* public or internal IP addresses
* domains tied to private infrastructure
* API keys or webhook URLs
* usernames
* customer identifiers
* hostnames
* sensitive agent naming
* unique internal file paths where they add no community value

## Affiliate disclosure

I deployed my Wazuh lab on [DigitalOcean](https://m.do.co/c/d6ad396822ca). Some future setup notes may reference [DigitalOcean](https://m.do.co/c/d6ad396822ca) using an affiliate link. If you choose to use it, I may receive a referral credit at no extra cost to you. Support is appreciated, but use whatever provider fits your environment.

## Contribution policy

Issues and curated pull requests are allowed, but this is not an open-ended community repo where every submission will be merged.

Security issues should be reported privately according to [SECURITY.md](SECURITY.md).

Contribution standards are documented in [CONTRIBUTING.md](CONTRIBUTING.md).