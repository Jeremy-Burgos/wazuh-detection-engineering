# Lists and CDB Notes

This repository uses lists to support selected rule workflows, including allowlists, deny lists, and IOC-style lookups.

The goal is to keep the examples useful without pretending that every public example file is a maintained intelligence source.

## Basic model

A Wazuh CDB-backed workflow has three parts:

1. the list file exists under `/var/ossec/etc/lists`
2. the list is registered in the Wazuh `<ruleset>` section
3. the rule uses a `<list ...>...</list>` lookup that matches the expected field and lookup type

If any one of those is missing, the workflow is incomplete.

## Common repository examples

Typical list categories in this repository include:

- malware hashes
- suspicious programs
- malicious IP examples
- malicious domain examples
- USB allowlists

## Example lookup patterns

Examples of the kind of logic these files support:

- hash match against a malware list
- program name match against a suspicious-programs list
- source IP match against an IP reputation list
- USB serial not present in an allowlist
- key-value matching for audit-related fields

## Public repository boundary

The `.example` files in this repository are examples.

They exist to show:

- format
- shape
- intended usage

They are not published as authoritative or continuously maintained feeds.

## Common mistakes

The most common mistakes with lists are:

- creating the file but not registering it in `<ruleset>`
- registering the list but never referencing it in a rule
- using the wrong field name in the rule
- using the wrong lookup type
- mixing incompatible value formats in the same list
- assuming a backup file proves the live ruleset is wired correctly

## Good practice

Keep list-backed logic simple.

For each list-backed rule, be able to answer:

- what field is being checked
- what list is being checked
- what a match means
- what a non-match means
- what the likely false positives are

