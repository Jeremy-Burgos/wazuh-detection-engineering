# Linux Auditd Notes

This repository uses Linux Auditd examples for two distinct detection themes:

- monitoring commands executed with root privileges
- detecting credential-access activity through targeted file-read events and command execution

These are related, but they are not the same use case.

## Root actions

The root-actions workflow uses Auditd `execve` rules filtered on `euid=0` to capture commands executed with effective root privileges.

A custom rule can be layered on top of the base Auditd event to make root-command alerts clearer and higher severity.

## Credential access

The credential-access workflow focuses on detecting:

- reads of `/etc/shadow`
- reads of `/etc/passwd`
- reads of shell history
- reads of SSH-related files
- suspicious command execution via Auditd and CDB lookups

That is why this repository separates:

- `rules/linux/root-actions-auditd.xml`
- `rules/linux/audit-keys-cdb.xml`
- `rules/linux/suspicious-programs-cdb.xml`

## Agent-side collection

For Auditd-driven detection to work, the endpoint must forward:

```xml
<localfile>
  <log_format>audit</log_format>
  <location>/var/log/audit/audit.log</location>
</localfile>
````

without that, the manager has nothing to evaluate.

