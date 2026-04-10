# ioc-builder

## Purpose

Document an IOC-building or IOC-updating workflow triggered by selected alerts.

## What it is meant to do

An IOC builder can take information from a qualifying alert and turn it into a more structured artifact, such as:

- a local IOC file
- a candidate indicator bundle
- a staging list for analyst review
- a follow-on enrichment target

## Why this is different

This is not the same as a blocking or cleanup action.

It is a content-generation or enrichment workflow, which means the main risks are:

- polluted IOC output
- low-confidence indicators being promoted too early
- over-collection of noisy values
- unstable downstream workflows

## Safe operating guidance

An IOC builder should usually be:

- narrow in scope
- tied to high-confidence fields
- reviewed before indicators are promoted to real enforcement
- treated as an analyst-assist workflow first

## Good candidates

Examples include:

- collecting repeated high-confidence malicious hashes
- capturing repeated hostile IPs after secondary validation
- building a review queue for suspicious process names or paths

## Bad candidates

Avoid building IOC artifacts from:

- weak single-signal events
- broad behavioral rules with noisy fields
- values that are easy to spoof
- fields that are not normalized

## Validation workflow

Before trusting an IOC-building workflow:

1. confirm the source fields are stable
2. confirm the output format is consistent
3. confirm duplicates are handled sensibly
4. confirm the workflow does not overwrite useful context
5. confirm a human can review the output

## Public repo stance

This repository documents the pattern and the cautions around it.

It does not ship a generic live IOC-building automation path as part of the initial public release.