# remove-threat

## Purpose

Document a threat-removal style active response, such as quarantining or removing a known artifact after a high-confidence detection.

## What it is meant to do

On a qualifying alert, Wazuh invokes a cleanup-oriented command such as `remove-threat`.

Depending on the environment, that could mean:

- deleting a known malicious file
- quarantining a file
- moving an artifact to an isolated path
- invoking a local remediation script

## Why this is risky

Cleanup is not neutral.

A bad cleanup action can:

- destroy evidence
- remove the wrong file
- break a legitimate application
- interfere with investigation and triage
- create inconsistent host state

## Safe use guidance

Use this only when:

- the detection is high confidence
- the target path is tightly scoped
- the workflow has been tested on the same platform
- the operational owner accepts the tradeoff between cleanup and evidence preservation

## Better default posture

In many environments, alerting plus triage is safer than automatic removal.

Detection-first is usually the better baseline.
Cleanup should come later, after validation and documentation.

## Validation workflow

Before enabling:

1. confirm the rule is stable and narrow
2. confirm the target artifact path is correctly populated
3. test on a disposable or lab host
4. verify the action only touches the expected object
5. document whether evidence is lost
6. define rollback or recovery steps

## Rollback

Rollback may include:

- disabling the response block
- restoring a quarantined file if appropriate
- reinstalling a broken application if the wrong object was touched
- updating the detection logic to avoid recurrence

## Public repo stance

This repository documents the concept and the risk model.

It does not publish generic destructive cleanup automation as part of the initial release.