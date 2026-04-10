# TESTED_ON

This repository is written against a real Wazuh deployment and then sanitized for publication.

## Core environment

- Wazuh manager: 4.14.4
- Wazuh indexer: 4.14.4
- Wazuh dashboard: 4.14.4
- Filebeat: 7.10.2
- Operating system: Ubuntu 24.04.4 LTS
- Kernel: Linux 6.8.0-106-generic
- Hosting: DigitalOcean
- Virtualization: KVM
- Topology: single all-in-one node
- Cluster block present in config: yes
- Cluster enabled: no

## Repository assumptions

This repository assumes:

- custom rules are stored under `/var/ossec/etc/rules`
- custom decoders are stored under `/var/ossec/etc/decoders`
- CDB lists are declared in the Wazuh `<ruleset>` section
- manager-side validation is performed before restart
- content is added incrementally, not dumped wholesale into production

## Live content categories observed in the source environment

- macOS persistence FIM rules
- macOS endpoint-oriented rules
- macOS USB monitoring with a CDB-backed allowlist check
- Linux AppArmor-related FIM rules
- FrigidStealer-specific decoders
- YARA decoding
- Osquery collection
- journald-based monitoring
- multiple IOC and CDB lists

## Important limitations

This repository is not documented as a Wazuh cluster guide.

This repository also does not claim that every detection pack has been exhaustively tuned across all environments. Some packs are baseline-oriented. Some are example-oriented. All should be validated before live use.