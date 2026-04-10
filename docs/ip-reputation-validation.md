# IP Reputation CDB Validation

This repository treats IP reputation as a separate CDB workflow from file-hash matching.

They are not the same use case and should not be mixed together.

## What this workflow does

A source IP is evaluated against a CDB-backed reputation list such as `blacklist-alienvault`.

If the source IP matches, a dedicated rule can raise an alert.

## Validation model

A clean validation flow looks like this:

1. confirm the reputation list is registered in the Wazuh ruleset
2. confirm the shared IP reputation rule exists
3. use a controlled source IP test case in a lab or replay workflow
4. confirm the event includes the expected `srcip` field
5. confirm the rule fires on a match

## What success looks like

Success means:

- the event includes a `srcip`
- the reputation rule checks the correct list
- the alert clearly indicates that the source IP matched the reputation list

