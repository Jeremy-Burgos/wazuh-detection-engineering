# disable-account

## Purpose

Document an account-disable active response that is only appropriate for narrow, high-confidence scenarios.

This is more sensitive than a detection-only workflow and should be treated carefully.

## What it is meant to do

On a qualifying alert, Wazuh invokes a command such as `disable-account` to disable a local account or otherwise prevent further account use.

## Why this is high risk

Disabling the wrong account can:

- lock out a legitimate user
- interrupt administrative access
- break automation
- create recovery work on a critical host

This is not a response to use casually.

## When it may make sense

Possible use cases include:

- repeated confirmed misuse of a disposable lab account
- controlled test environments
- high-confidence compromise of a narrowly scoped local account
- tightly managed systems with clear rollback procedures

## When it does not make sense

Avoid this response when:

- account identity is ambiguous
- the event source is noisy
- the account may be shared
- the host is business-critical
- rollback is unclear or slow

## Validation workflow

Before enabling:

1. confirm the triggering rule is stable
2. confirm the event contains the exact account field you expect
3. confirm the command only targets the intended account scope
4. test on a non-critical host first
5. test rollback immediately after the test
6. document the operational side effects

## Rollback

Rollback should be explicit and documented before deployment.

That usually means:

- disable the active-response block
- validate and restart the manager
- restore the disabled account manually using the platform’s account-management tooling
- confirm access is restored

## Public repo stance

This repository documents the safety model for account-disable responses.

It does not recommend broad deployment of this pattern without strict operating constraints.