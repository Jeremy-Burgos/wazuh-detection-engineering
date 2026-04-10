# Installation on the Wazuh Manager

This repository assumes manual placement on the Wazuh manager.

That is the intended operating model.

The goal is to keep every change visible, reviewable, and easy to roll back.

## Scope

This guide covers:

- where rules go
- where decoders go
- how list-backed content fits into the Wazuh configuration
- how to validate before restart

It does not cover full Wazuh installation from scratch.

## Expected paths

Typical manager-side paths:

- custom rules: `/var/ossec/etc/rules`
- custom decoders: `/var/ossec/etc/decoders`
- lists: `/var/ossec/etc/lists`
- main config: `/var/ossec/etc/ossec.conf`

## General placement model

### Rules

Place repository rules into:

```bash
/var/ossec/etc/rules
````

Examples:

* `rules/macos/950-macos-persistence-fim.xml`
* `rules/linux/linux-persistence-techniques.xml`

### Decoders

Place repository decoders into:

```bash
/var/ossec/etc/decoders
```

Examples:

* `decoders/shared/yara_decoder.xml`
* `decoders/linux/udev_usb_decoder.xml`

### Lists

List files belong under:

```bash
/var/ossec/etc/lists
```

If you use a subdirectory layout privately, keep the Wazuh `<ruleset>` registration aligned to the real file path.

## Registering CDB lists

A list file on disk is not enough.

If a rules file references a CDB list, that list must also appear in the Wazuh `<ruleset>` section in `ossec.conf`.

Example pattern:

```xml
<ruleset>
  <decoder_dir>ruleset/decoders</decoder_dir>
  <rule_dir>ruleset/rules</rule_dir>

  <decoder_dir>etc/decoders</decoder_dir>
  <rule_dir>etc/rules</rule_dir>

  <list>etc/lists/usb-drives</list>
  <list>etc/lists/malware-hashes</list>
</ruleset>
```

## Recommended workflow

1. Back up the current file you will change
2. Copy one new rules file or one new decoder file into place
3. If list-backed logic is involved, confirm the list is registered in `<ruleset>`
4. Validate the manager configuration
5. Test with `wazuh-logtest` where appropriate
6. Restart the manager
7. Confirm the expected result before adding more content

## Example copy workflow

```bash
sudo cp rules/linux/linux-persistence-techniques.xml /var/ossec/etc/rules/
sudo cp decoders/shared/yara_decoder.xml /var/ossec/etc/decoders/
```

## Validation commands

Run these before restart:

```bash
sudo /var/ossec/bin/wazuh-syscheckd -t
sudo /var/ossec/bin/wazuh-logcollector -t
sudo /var/ossec/bin/wazuh-modulesd -t
sudo /var/ossec/bin/wazuh-analysisd -t
```

For decoder and rule testing:

```bash
sudo /var/ossec/bin/wazuh-logtest
```

## Restart

Restart only after validation passes:

```bash
sudo systemctl restart wazuh-manager
sudo journalctl -u wazuh-manager -n 80 --no-pager
```

## What not to do

Do not:

* copy the entire repository into `/var/ossec/etc`
* deploy multiple new packs at once
* publish or load backup files
* mix broken experiments with live content
* assume a list is active just because the file exists