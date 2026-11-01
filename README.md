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

## What has been measured

In EB006, a live LLM agent with one tool ("create a GitHub issue") read a note containing a hidden instruction to file an unauthorized second issue.

- With no guard, gpt-oss-120b and gpt-oss-20b followed it in all 10 trials each; qwen3.8-27b followed it in none.
- A check that looked only at the authorized issue passed all 10 gpt-oss-120b trials while an unauthorized issue existed. A separate read-only observer, which never reads the agent's own log, caught every one.
- With a pre-execution guard on, the model still tried every time, but zero unauthorized issues existed, confirmed by the observer.

One injection wording, 10 trials per model. Failed and excluded runs are listed in the write-up. Details: [EB006_RESULTS.md](https://github.com/gokuljayaprakash8/kalpang-observer/blob/main/EB006_RESULTS.md)

## Pilot

**Introductory price: $300 per workflow, for the first three teams.** Delivery within five working days after scope, access and test setup are agreed.

Scope: one workflow, one authorized action, with effects readable through an API. The workflow runs in CI or in a sandbox, mock or containerized repo you share. No production access is needed. My observer uses its own short-lived, read-only credential, deleted after the engagement. Scope is confirmed in writing before any payment.

## Who this is for

Teams building agents that act on GitHub first: coding agents and bots that create or change issues, pull requests or files.

## Evidence so far

- [EB006 results](https://github.com/gokuljayaprakash8/kalpang-observer/blob/main/EB006_RESULTS.md): a live LLM agent, three models, 10 trials each; an independent observer caught effects that a target-only check passed.
- [EB005 results](https://github.com/gokuljayaprakash8/kalpang-observer/blob/main/EB005_RESULTS.md): a valid chain was admitted and the observer still flagged an unapproved effect; a widened chain was refused.
- [aat-vectors](https://github.com/gokuljayaprakash8/aat-vectors): 43 test vectors and an independent checker for delegation rules.

## What is true today

- Built with substantial LLM assistance. Every result is a run you can repeat, so you do not have to trust me or the model.
- Public demos: EB005 uses a scripted workflow. EB006 uses a live LLM agent (three models, 10 trials each, one injection wording), with real GitHub effects checked by a separate observer. Neither is a claim about agents in general. Both ran under one GitHub account, so they show the method, not a separate trust domain.
- "Independent" here means done by someone outside your dev team, with a separate read-only identity. It is not independent of GitHub itself.
- Not a penetration test, a full security audit, a certification, or a guarantee. Results cover only the tested workflow, scenarios and evidence.

## Authorization and scope

I test only systems you own or have authorized me in writing to test.

## How to start

In writing only: open an issue in this repository or message [@invariantdesign](https://x.com/invariantdesign) on X. Scope is agreed in writing before any payment.

## Contact

**Gokul Jayaprakash**
Email: gokuljayaprakashnair@gmail.com
