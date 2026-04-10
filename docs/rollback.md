# Rollback

Rollback should be simple, fast, and boring.

If a change creates parser errors, alert floods, broken decoding, or operational risk, remove it quickly and return to the last known-good state.

## General rollback rules

- Do not troubleshoot a broken production manager in place for too long.
- Remove the last change first.
- Restore the previous file from backup.
- Revalidate before restarting again.
- Roll back one pack at a time.

## Before making any change

Always create a backup first.

Examples:

```bash
sudo cp /var/ossec/etc/ossec.conf /var/ossec/etc/ossec.conf.bak.$(date +%F-%H%M%S)
sudo cp /var/ossec/etc/rules/example.xml /var/ossec/etc/rules/example.xml.bak.$(date +%F-%H%M%S)
sudo cp /var/ossec/etc/decoders/example.xml /var/ossec/etc/decoders/example.xml.bak.$(date +%F-%H%M%S)
````

## Roll back a rules file

If a new rules file causes problems:

1. Remove or rename the file from `/var/ossec/etc/rules`
2. Restore the previous version if needed
3. Validate the configuration
4. Restart the manager
5. Confirm the issue is gone

Example:

```bash
sudo mv /var/ossec/etc/rules/linux-malware-koske.xml /var/ossec/etc/rules/linux-malware-koske.xml.disabled
sudo /var/ossec/bin/wazuh-analysisd -t
sudo systemctl restart wazuh-manager
```

## Roll back a decoder file

If a decoder causes parsing problems or field extraction issues:

1. Remove or rename the file from `/var/ossec/etc/decoders`
2. Validate with `wazuh-analysisd -t`
3. Re-test with `wazuh-logtest`
4. Restart the manager if needed

Example:

```bash
sudo mv /var/ossec/etc/decoders/udev_usb_decoder.xml /var/ossec/etc/decoders/udev_usb_decoder.xml.disabled
sudo /var/ossec/bin/wazuh-analysisd -t
sudo systemctl restart wazuh-manager
```

## Roll back a list-backed change

If a rule depends on a CDB list and the behavior is wrong:

1. Disable or remove the rule first
2. Confirm the list path in `<ruleset>`
3. Restore the previous list file if the list contents changed
4. Restart the manager after validation

Do not change both the rule and the list at the same time unless you are prepared to undo both.

## Roll back an `ossec.conf` change

If the manager throws config warnings or fails to start cleanly:

1. Restore the backup of `ossec.conf`
2. Validate each component again
3. Restart the manager
4. Review the journal and `ossec.log`

Example:

```bash
sudo cp /var/ossec/etc/ossec.conf.bak.YYYY-MM-DD-HHMMSS /var/ossec/etc/ossec.conf
sudo /var/ossec/bin/wazuh-syscheckd -t
sudo /var/ossec/bin/wazuh-logcollector -t
sudo /var/ossec/bin/wazuh-modulesd -t
sudo /var/ossec/bin/wazuh-analysisd -t
sudo systemctl restart wazuh-manager
```

## Roll back active-response changes

Active response has a larger blast radius than ordinary detection logic.

If an active-response change behaves badly:

1. disable the active-response block in `ossec.conf`
2. validate the config
3. restart the manager
4. confirm the response no longer triggers
5. review whether any host-level side effects need manual cleanup

Treat active-response rollback as an operational issue, not just a content issue.

## When to stop and revert fully

Stop tuning and revert immediately if you see:

* manager start failures
* repeated config warnings after a change
* major alert floods
* broken decoding across unrelated events
* endpoint-side operational impact
* blocking actions that hit the wrong targets

## Rollback notes

For each rollback, record:

* what changed
* what failed
* how it was reverted
* what validation passed after rollback
* whether the content needs redesign instead of a small fix