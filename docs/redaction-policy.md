# Redaction Policy

This repository is public. The content must be useful without exposing private environment details.

The rule is simple:

keep the technical logic, remove the identifying detail.

## Always remove

Do not publish:

- public IP addresses tied to your infrastructure
- internal IP addresses
- private domains
- private hostnames
- usernames tied to real people or systems
- customer names
- API keys
- webhook URLs
- bearer tokens
- token formats that reveal operational details
- agent names that expose internal naming conventions
- raw file paths unique to private environments when they add no public value
- unredacted screenshots with sensitive values visible

## Usually remove

These are often better replaced with safe placeholders:

- serial numbers
- device identifiers
- sample hashes from private investigations
- email addresses
- private network ports when unnecessary
- exact droplet or node identifiers
- alert payloads that expose private environment context

## Safe replacements

Use clear placeholders such as:

- `YOUR_API_KEY`
- `YOUR_WEBHOOK_URL`
- `example.internal`
- `NODE_IP`
- `HOSTNAME_REDACTED`
- `SERIAL_REDACTED`
- `198.51.100.10`
- `203.0.113.44`

Use documentation-safe example ranges and domains where possible.

## Rules for screenshots

Before publishing a screenshot, confirm that it does not show:

- private IPs
- private URLs
- real usernames
- hostnames
- agent IDs you do not want exposed
- raw API responses with sensitive content
- browser history or tabs
- terminal prompts that expose private infrastructure

If a screenshot needs too much blurring, do not publish it. Recreate a cleaner one instead.

## Rules for sample alerts and logs

Redacted samples should preserve:

- the event shape
- the relevant field names
- the rule or decoder logic
- the reason the event matters

Redacted samples should not preserve:

- private identifiers
- secrets
- unnecessary timestamps tied to private operations
- exact network topology

## Rules for IOC examples

IOC example files in this repository should be clearly marked as examples when they are not maintained feeds.

Do not publish private indicators from a real investigation unless you are certain they are safe and appropriate to disclose.

## Backup and broken files

Never publish:

- `.bak` files
- `.save` files
- `.broken` files
- emergency scratch files
- exports that were only used for troubleshooting

A clean public repository should only contain intentional files.

## Redaction review checklist

Before publishing any file or screenshot, ask:

1. Does this expose anything unique to my environment?
2. Does this include a secret or credential?
3. Does this reveal an internal naming pattern?
4. Does this create unnecessary operational exposure?
5. Can the same technical value be preserved with a placeholder?

If the answer to any of the first four is yes, redact or replace it.

## Editorial standard

Redaction should not make the repository vague or useless.

The goal is not to strip all detail. The goal is to preserve the engineering value while removing what should remain private.