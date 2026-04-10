# Troubleshooting

This file covers the kinds of practical problems that show up when building and testing custom Wazuh content.

It is intentionally direct.

## 1. `Invalid element in the configuration: 'integration'`

Symptom:

```text
wazuh-syscheckd: WARNING: (1230): Invalid element in the configuration: 'integration'
````

What it usually means:

An `<integration>` block is placed inside the wrong section in `ossec.conf`, often inside `<syscheck>` instead of as a top-level child of `<ossec_config>`.

Fix:

* move the `<integration>` block out of `<syscheck>`
* place it directly under `<ossec_config>`
* validate again with:

```bash
sudo /var/ossec/bin/wazuh-syscheckd -t
```

## 2. `netstat not available. Skipping port check.`

Symptom:

```text
wazuh-syscheckd: INFO: netstat not available. Skipping port check.
```

What it usually means:

A command-monitoring or related local check still depends on `netstat`, but the host does not have it installed.

Fix:

* either install the missing tool if you intentionally depend on it
* or replace the old command with a cleaner modern equivalent such as `ss -tulpn`

## 3. A list file exists but the rule never seems to use it

Common causes:

* the list is not registered in `<ruleset>`
* the rule references the wrong path
* the rule uses the wrong field name
* the lookup type does not match the data
* the only working version is trapped in a backup or broken file, not the active ruleset

Check:

* list registration in `ossec.conf`
* active rule file contents
* `wazuh-logtest` output
* whether you are accidentally looking at `.bak` or `.broken` artifacts

## 4. A decoder exists but fields do not extract as expected

Common causes:

* the sample log format does not actually match the regex
* the wrong parent decoder is hit
* the program name or prematch is too broad
* a duplicate decoder name creates confusion

Check:

```bash
sudo /var/ossec/bin/wazuh-logtest
```

Use a real or controlled sample and verify the exact decoder path and fields.

## 5. A rules file loads but produces alert floods

Common causes:

* the path or source is broader than intended
* the grouping logic is too loose
* a list-backed match is too permissive
* the baseline event is normal in the environment

Fix:

* tighten the field match
* reduce the scope
* add better parent logic
* document the tuning requirement
* roll back if needed and redesign the pack instead of patching blindly

## 6. A change broke the manager startup flow

Do not keep improvising.

Do this:

1. restore the last known-good file
2. rerun the validation commands
3. restart the manager
4. review the journal and `ossec.log`
5. reintroduce the change in smaller pieces

## 7. The repository tree starts getting noisy

This is a maintenance problem, not just a cosmetic one.

Remove or refuse:

* `.bak` files
* `.save` files
* `.broken` files
* scratch exports
* duplicated packs
* files with unclear purpose

A clean public ruleset is part of operational quality.

## 8. Unsure whether something belongs in a rule or a decoder

Use this test:

* if the source is not being parsed into the fields you need, start with the decoder
* if the fields already exist and you need detection logic, start with the rule
* if neither is stable, stop and gather better sample data first