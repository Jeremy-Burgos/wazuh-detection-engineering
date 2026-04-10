# Active Response Safety

Active response should be treated as operational content, not just detection content.

A bad rule can create alert noise.
A bad active-response workflow can block legitimate traffic, lock out an account, or create host-level recovery work.

## Baseline rule

Document first. Automate second.

This repository starts from a documentation-first posture for active response because the operational blast radius is higher than ordinary rules or decoders.

## Typical active-response use cases

Examples include:

- dropping a source IP
- disabling an account
- removing a threat artifact
- invoking a malware cleanup workflow
- building or updating an IOC artifact
- triggering a notification or escalation path

## Why active response is riskier

Active response can:

- block the wrong source
- trigger off false positives
- break access to a service
- create repeated actions from noisy rules
- leave partial state behind after failure
- behave differently across operating systems

## Preconditions before enabling any response

Before enabling an active-response workflow, confirm:

1. the triggering rule is stable
2. false positives are understood
3. test conditions are controlled
4. rollback steps are documented
5. timeout behavior is understood
6. allowlist and exclusion logic are defined where needed

## Safe test model

Test in a controlled environment first.

Use this order:

1. validate the detection logic
2. confirm the trigger is correct
3. run the response in a lab or narrow test path
4. document the side effects
5. confirm cleanup or rollback
6. only then consider broader use

## Recommended documentation for each response

Each active-response workflow documented in this repository should include:

- purpose
- trigger conditions
- execution location
- scope of action
- timeout or persistence behavior
- common failure cases
- rollback steps
- false positive risk

## Common bad patterns

Avoid:

- broad firewall responses tied to noisy rules
- account disable actions without clear identity validation
- cleanup actions that destroy evidence
- response logic that depends on untrusted fields
- publishing scripts before the operating assumptions are documented