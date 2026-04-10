# Active Response Mapping

This file documents the active-response surface represented by the repository.

The repository does not need to publish every executable script to document the capability professionally.

## Commands represented

The live environment behind this repository includes manager-side command definitions for:

- `disable-account`
- `firewall-drop`
- `remove-threat`
- `yara_linux`
- `ioc-builder`

## Representative trigger mapping

A curated example mapping is:

- `firewall-drop`
  - example trigger: repeated hostile or attack-oriented rules
  - execution: local
  - timeout: environment-specific

- `disable-account`
  - example trigger: account misuse or brute-force threshold rule
  - execution: local
  - timeout: defined where needed

- `remove-threat`
  - example trigger: high-confidence malicious file or related alert
  - execution: local

- `yara_linux`
  - example trigger: file-related rules that warrant a YARA follow-on
  - execution: local

- `ioc-builder`
  - example trigger: selected high-confidence alerts worth promoting into IOC review
  - execution: server

## Publication stance

The repository documents active response conservatively.

It treats active response as operational content with real blast radius, not as a casual add-on.