# Decoders

This directory contains custom decoders.

A custom decoder should exist only when it solves a real parsing problem. Do not create one just because a source is unfamiliar. If Wazuh already parses the source well enough, keep the repo simpler and use the built-in behavior.

## Layout

- `common/` contains reusable decoders that support multiple packs or general workflows
- `macos/` contains macOS-specific decoding logic
- `linux/` contains Linux-specific decoding logic only where custom parsing is genuinely needed

## Decoder design goals

Decoders in this repository should be:

- narrow in scope
- easy to understand
- easy to test with sample events
- named clearly
- free from duplicate decoder names

## When to create a decoder

Create a decoder when:

- the log format is custom or non-standard
- important fields are not extracted by default
- a rule depends on fields that do not already exist
- a threat-specific example needs custom parsing

## When not to create a decoder

Do not create a decoder when:

- the log source is already parsed well enough by Wazuh
- the parsing logic is only a guess
- the source format is unstable and untested
- you are trying to force structure where no real sample data exists

## Testing

Every decoder should be tested against real or synthetic sample data.

Use `wazuh-logtest` and confirm:

- the intended decoder name is hit
- the right fields are extracted
- parent-child relationships behave as expected
- the decoded fields support the rule logic cleanly

## File discipline

Do not mix unrelated decoder families into one giant file.

Keep one file per logical purpose where possible, for example:

- YARA output decoding
- journald CRON parsing
- journald Docker parsing
- resource health logs
- threat-specific macOS parsing

