# firewall-drop

## Purpose

Document a firewall-based active response that blocks a source IP after a qualifying alert.

This is one of the most common active-response patterns in Wazuh. It is also one of the easiest to misuse.

## What it is meant to do

On a qualifying alert, the manager or agent invokes a firewall-related command such as `firewall-drop` to block the source IP for a defined period.

Typical use cases include:

- repeated brute-force attempts
- repeated hostile connection attempts
- IPs already matched by a reputation workflow
- narrowly scoped high-confidence alerts

## Where it can run

This depends on your Wazuh configuration.

Common patterns are:

- manager-side execution
- local execution on the affected agent
- all-agent execution in tightly controlled environments

The safest starting point is usually a narrow manager-side or local-only deployment, not broad multi-host action.

## Why this is risky

A false positive here can block:

- a legitimate user
- a shared upstream NAT
- a monitoring system
- a VPN egress IP
- an internal scanner you forgot to allowlist

Blocking the wrong address can create more operational damage than the original event.

## Safe trigger guidance

Do not bind this response to low-confidence alerts.

Safer candidates include:

- repeated authentication failures with clear source attribution
- IP reputation matches combined with another signal
- repeated malicious behavior over a short time window
- tightly scoped externally sourced attack events

## Timeout guidance

Prefer temporary blocking over indefinite blocking.

A temporary block is easier to reason about, easier to test, and easier to reverse if the trigger was wrong.

## Validation workflow

Before enabling:

1. validate the triggering rule
2. confirm the source IP field is populated as expected
3. test in a lab or controlled host
4. confirm the firewall command works on the target operating system
5. confirm the timeout behaves as expected
6. confirm rollback works

## Rollback

If the response behaves badly:

1. disable the active-response block in `ossec.conf`
2. validate the config
3. restart the manager
4. remove any temporary block manually if needed
5. redesign the trigger before trying again

## Public repo stance

This repository documents the workflow and the safety model.

It does not publish a drop-in firewall automation pack as part of the initial release.