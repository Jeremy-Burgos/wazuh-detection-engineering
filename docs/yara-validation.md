# YARA Validation

This repository treats YARA as a staged detection workflow, not a blind automation path.

## Validation goals

The goal is to prove that:

- FIM detects the file change
- the source YARA trigger rules fire
- the `yara_linux` active response executes
- the active response writes a result to `active-responses.log`
- the YARA decoder parses the result
- the positive-match rule fires

## Validation model

A clean validation flow looks like this:

1. confirm the monitored Linux directory is present under `<syscheck>`
2. confirm the `yara_linux` command exists in manager configuration
3. confirm the active-response block points to the correct trigger rule IDs
4. place a controlled test file into the monitored directory
5. confirm the file event triggers FIM
6. confirm `active-responses.log` contains a `wazuh-yara: INFO - Scan result:` line
7. confirm the YARA decoder and positive-match rule raise an alert

## What success looks like

Success means:

- the file event triggered a source rule
- the active response executed
- the YARA log line was decoded
- the positive-match rule fired with the expected `yara_rule` and `yara_scanned_file` fields

