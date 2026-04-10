# WordPress SCA Validation

This repository treats the WordPress assessment example as an SCA workflow, not a detection rule pack.

## Validation goals

The goal is to prove that:

- the policy file loads correctly
- the agent includes the policy in its SCA configuration
- the endpoint meets the policy requirements
- the checks execute and produce results
- the results are readable and explainable

## Validation model

A clean validation flow looks like this:

1. place the policy file on the Linux WordPress host outside the default Wazuh ruleset path
2. set ownership so the Wazuh agent can read it
3. reference the policy in the agent `<sca>` configuration
4. restart the Wazuh agent if needed
5. confirm the policy appears in SCA results
6. review pass and fail results for each check

## What success looks like

Success means:

- the policy is loaded
- the requirements pass
- each check returns a result
- the findings are meaningful and map to real hardening work