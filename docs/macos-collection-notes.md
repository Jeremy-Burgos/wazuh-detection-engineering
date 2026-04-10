# macOS Collection Notes

This repository separates macOS content into two layers:

- agent-side collection
- manager-side decoding and rules

That split matters.

The manager can only evaluate what the macOS agent forwards.

## Collection areas represented in this repository

The macOS side of this repository is organized around three collection themes:

1. endpoint-oriented event visibility
2. resource monitoring
3. USB device monitoring

## Endpoint-oriented visibility

The macOS endpoint rules are intended to work with a filtered event collection model rather than a blind dump of everything.

The goal is to collect security-relevant macOS events in a controlled way and then evaluate them with focused manager-side rules.

## Resource monitoring

The resource-monitoring decoder family in this repository expects structured command-output style events for:

- CPU health
- memory health
- disk health
- CPU metrics
- load average
- memory metrics
- disk metrics
- network metrics

These are best kept as a dedicated macOS collection workflow, not mixed into unrelated host telemetry.

## USB monitoring

The macOS USB monitoring rule pack depends on a JSON-formatted log source that records connection and disconnection events, including the device serial number used by the CDB allowlist workflow.

If the serial field is not present, the allowlist logic will not behave as intended.

## Public repo rule

This repository documents the structure and examples for macOS collection.

It does not publish private environment details, private device identifiers, or raw lab telemetry.