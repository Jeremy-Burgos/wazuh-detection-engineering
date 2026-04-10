# Active Response

This directory documents active-response design and safety considerations for the repository.

It does not publish executable helper scripts in the initial public version.

That is intentional.

## Why this directory exists

Active response is operationally different from ordinary detection content.

A bad rule can create noise.
A bad active-response workflow can block hosts, disrupt users, or create recovery work.

This repository documents the logic, risks, and safe usage model without pretending that every environment should copy scripts directly.

## Current publication stance

For the initial public release:

- active-response concepts are documented
- operational guidance is included
- blast radius is discussed
- rollback is discussed
- executable helper scripts are not published by default

## Why scripts are not published first

Active-response scripts are highly environment-sensitive.

They often depend on:

- local firewall behavior
- host-level tooling
- endpoint operating system differences
- response timeout design
- allowlist logic
- safe test conditions

Publishing them too early can make the repository look larger, but also less responsible.

## What belongs here

This directory should contain markdown files such as:

- `firewall-drop.md`
- `disable-account.md`
- `remove-threat.md`
- `yara_linux.md`
- `ioc-builder.md`

Each file should explain:

- what the response is meant to do
- what triggers it
- where it runs
- what could go wrong
- how to test it safely
- how to roll it back

## Operating principle

Detection is easier to recover from than automated response.

If there is doubt, document first, automate later.