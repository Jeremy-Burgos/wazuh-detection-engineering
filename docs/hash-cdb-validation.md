# Hash CDB Validation

This repository includes a documented CDB-backed file-hash workflow.

The goal is to prove that:

- file hashes are being recorded by FIM
- the hash lists are registered in the Wazuh ruleset
- the manager has active rules that use those lists
- a controlled file event can trigger a real alert

## What is already represented

The repository includes shared hash CDB rules for:

- SHA256 hash matching against `malware-hashes`
- MD5 hash matching against `malware-hashes-md5`
- SHA256 hash matching against `malware-hashes-koske`

## Validation model

A clean validation flow looks like this:

1. create a benign test file
2. calculate its SHA256 and MD5 values
3. add those values to validation lists or a controlled lab list
4. validate the manager config
5. restart the manager
6. create or modify the file in a monitored FIM path
7. confirm the alert fired

## What success looks like

Success means:

- the event contains file-hash fields
- the shared hash CDB rule fires
- the alert clearly identifies the file path and the matching hash workflow

