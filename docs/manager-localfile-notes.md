# Manager Localfile Notes

This repository includes manager-side examples for command-driven localfile monitoring.

That is a practical part of the setup and worth documenting because it adds real operational value.

## Current collection themes represented

The manager-side command examples in this repository focus on:

- filesystem capacity
- listening ports
- recent login history

## Example command categories

Representative examples include:

- `df -P`
- `ss -tulpn`
- `last -n 20`

These are not meant to be exhaustive system telemetry. They are small, useful visibility checks that can support focused decoder and rule logic.

## Why this belongs in the repo

This content shows that the repository is not only about static rules and lists.

It also demonstrates manager-side host visibility and simple command-output workflows that can be decoded and alerted on cleanly.

