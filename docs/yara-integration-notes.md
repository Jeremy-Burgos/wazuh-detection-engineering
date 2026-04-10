# YARA Integration Notes

This repository includes a Linux-focused YARA workflow built around Wazuh FIM and Active Response.

## How the workflow works

The workflow is:

1. Wazuh FIM monitors a Linux path for new or modified files
2. a source rule fires when a file is added or modified
3. the `yara_linux` active response runs `yara.sh`
4. YARA writes results to `active-responses.log`
5. custom decoders parse the result
6. follow-on rules raise an alert for positive matches

## Why this repository keeps it Linux-focused

The official Wazuh documentation covers both Linux and Windows.

This repository is intentionally scoped to Linux and macOS only, so the public YARA example stays Linux-focused.

## Repository components for YARA

This repository uses:

- `rules/linux/yara-fim-detection.xml`
- `decoders/shared/yara_decoder.xml`
- `active-response/yara_linux.md`
- `examples/agent/linux-yara-fim.example.xml`

