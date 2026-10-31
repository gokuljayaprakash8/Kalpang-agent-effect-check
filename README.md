# KALPANG Agent Effect Check

**Did your agent's real-world effect stay inside what it was allowed to do? I check, and I give you the test to rerun.**

Most agent testing asks whether an attacker can trick the model. This asks something different: after the agent acted, did anything happen beyond what was authorized?

A check that reads only the one thing the agent was supposed to change can pass while the agent also did something else. In my own live experiment (EB004), the authorized issue matched exactly, so a check of that issue alone would have passed. A scan of everything inside the declared boundary found one extra issue nobody had authorized. [Details](https://github.com/gokuljayaprakash8/kalpang-observer)

## What you get

1. **A rerunnable test** (a GitHub Actions workflow and scripts) for your workflow, so you can run it again whenever you change the agent.
2. **A short written report:** what was authorized, what was observed, a verdict per scenario, and what the check could not see.
3. **Evidence:** raw logs, API responses, IDs, timestamps and hashes.

## Four scenarios

1. **Normal run:** the authorized action happens and nothing else.
2. **Extra effect:** an additional, unapproved action appears.
3. **No authority:** an action happens without valid authorization behind it.
4. **Widened delegation:** delegated authority exceeds what its parent allowed.

If a scenario does not apply to your setup (for example, there is no parent-child delegation), the report says "not applicable". It never claims a pass.

## Pilot

**Introductory price: $300 per workflow, for the first three teams.** Delivery within five working days after scope, access and test setup are agreed.

Scope: one workflow, one authorized action, with effects readable through an API. The workflow runs in CI or in a sandbox, mock or containerized repo you share. No production access is needed. My observer uses its own short-lived, read-only credential, deleted after the engagement. Scope is confirmed in writing before any payment.

## Who this is for

Teams building agents that act on GitHub first: coding agents and bots that create or change issues, pull requests or files.

## Evidence so far

- [EB005 results](https://github.com/gokuljayaprakash8/kalpang-observer/blob/main/EB005_RESULTS.md): a valid chain was admitted and the observer still flagged an unapproved effect; a widened chain was refused.
- [aat-vectors](https://github.com/gokuljayaprakash8/aat-vectors): 43 test vectors and an independent checker for delegation rules.

## What is true today

- Built with substantial LLM assistance. Every result is a run you can repeat, so you do not have to trust me or the model.
- My public demos use a scripted workflow, not an LLM agent, and ran under one GitHub account. They show the method. They do not show a separate trust domain.
- "Independent" here means done by someone outside your dev team, with a separate read-only identity. It is not independent of GitHub itself.
- Not a penetration test, a full security audit, a certification, or a guarantee. Results cover only the tested workflow, scenarios and evidence.

## Authorization and scope

I test only systems you own or have authorized me in writing to test.

## Contact

**Gokul Jayaprakash**
Email: gokuljayaprakashnair@gmail.com
