# Validation

This repository is built around manual review, deliberate placement, and validation before restart.

Do not copy multiple packs into a live Wazuh manager and restart blindly.

## Validation goals

Every change should answer these questions:

- Does the XML parse cleanly?
- Does the manager accept the configuration?
- Does the decoder extract the intended fields?
- Does the rule fire on the expected event?
- Does the rule avoid obvious false positives in the target environment?
- Does any referenced CDB list exist and appear in the Wazuh `<ruleset>` section?

## Pre-change checklist

Before adding or changing a file:

1. Back up the current Wazuh configuration and any file you plan to replace.
2. Add one rules file or one decoder file at a time.
3. Confirm any referenced list path is registered in the `<ruleset>` section of `ossec.conf`.
4. Check for duplicate rule IDs and duplicate decoder names.
5. Make sure no backup or broken files are mixed into the active ruleset.

## Core validation commands

Validate the manager-side configuration components before restart.

```bash
sudo /var/ossec/bin/wazuh-syscheckd -t
sudo /var/ossec/bin/wazuh-logcollector -t
sudo /var/ossec/bin/wazuh-modulesd -t
sudo /var/ossec/bin/wazuh-analysisd -t
````

If you are validating rules and decoders against sample logs, use:

```bash
sudo /var/ossec/bin/wazuh-logtest
```

## Recommended validation flow

Use this order:

1. Copy the new file into `/var/ossec/etc/rules` or `/var/ossec/etc/decoders`
2. Confirm list registration if the content uses `<list ...>...</list>`
3. Run the daemon validation commands
4. Run `wazuh-logtest` with a controlled sample if the content is log-driven
5. Restart the manager only after validation succeeds
6. Confirm expected behavior in alerts or logs
7. Record any tuning notes

## Rule validation

For rules that depend on FIM:

* confirm the monitored path is actually under `syscheck`
* make one controlled file change
* confirm the expected rule triggers
* confirm the alert message is useful and not too broad

For rules that depend on hashes:

* confirm the list path exists
* confirm the hash format matches the list format
* test with a safe sample or lab artifact
* make sure the rule does not trigger on malformed fields

For rules that depend on CDB allowlists or deny lists:

* confirm the list is loaded through `<ruleset>`
* confirm the lookup type matches the field type
* test both a matching case and a non-matching case

## Decoder validation

For custom decoders:

* test with a real or synthetic sample log line
* confirm the intended decoder name is hit
* confirm the expected extracted fields appear in `wazuh-logtest`
* avoid creating duplicate decoder names or ambiguous parent chains

## Post-restart checks

After restart, review recent manager output:

```bash
sudo systemctl restart wazuh-manager
sudo journalctl -u wazuh-manager -n 80 --no-pager
sudo tail -n 80 /var/ossec/logs/ossec.log
```

If integrations are involved, also check:

```bash
sudo tail -n 80 /var/ossec/logs/integrations.log 2>/dev/null || true
```

## What to watch for

Common validation failures include:

* invalid XML
* duplicate rule IDs
* duplicate decoder names
* list path not loaded in `<ruleset>`
* wrong field name in a `<list>` lookup
* invalid nesting in `ossec.conf`
* content copied into the wrong directory
* sample logs that do not match the expected log format
* alert logic that is too broad

## Validation record

For any significant change, keep a short record:

* file changed
* purpose
* test method
* sample used
* result
* false positive notes
* rollback path

That keeps the repository honest and makes future tuning easier.