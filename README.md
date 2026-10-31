# Kalpang-agent-effect-check

# Agent Effect Check

**An independent, evidence-based check of whether an AI agent's actions stayed within its authorization.**

Agent Effect Check assesses one AI-agent workflow and one authorized action through four controlled scenarios. The goal is to identify observable mismatches between what was authorized and what the workflow actually did.

## What you get

For one workflow, I run four scenarios:

1. **Normal run:** The authorized action occurs, with no additional unauthorized effect observed.
2. **Extra effect:** An additional, unapproved action appears.
3. **No authority:** An action occurs without valid authorization behind it.
4. **Widened delegation:** Delegated authority exceeds what its parent authorization permits.

The engagement includes:

- A written report describing the setup, observations, verdicts, and limitations.
- A reproducible repository your team can use to rerun the test.
- Evidence supporting the reported results.
- A plain-language account of what the assessment does and does not establish.

Verdicts apply to the tested scenarios and observed evidence. They are not a guarantee that other unauthorized effects cannot occur.

## Pilot offer

**Price: $300 per workflow**

Scope: I accept workflows where the effect can be read back through an API and the workflow can run in a CI job or sandbox I access through a repo you share. I confirm the scope in writing before any payment.

**Delivery: within five working days**, once the scope and required access or materials have been agreed.

The pilot covers one defined workflow and one authorized action, evaluated against the four scenarios above. Any additional workflows or materially expanded scope are agreed separately.

## Who this is for

Teams developing AI agents that can create or modify issues, open pull requests, write files, call tools, or trigger other external actions.

The central question is: **did the observed actions remain within the authority granted to the agent?**

## Sample results

Read the example report: [EB005: Results and limitations](https://github.com/gokuljayaprakash8/kalpang-observer/blob/main/EB005_RESULTS.md)

The report documents a real experiment and its limitations. Read it as evidence from a bounded demonstration, not as proof of comprehensive security.

## Method and limitations

This work is developed with substantial assistance from large language models. Claims in reports are tied to reproducible test results wherever applicable.

My earlier demonstration used a scripted workflow in place of an LLM agent, with real effects on GitHub (real issues, created by a real workflow). The executor, the gateway and the observer ran under one GitHub account, so it did not establish a separate trust domain between the tested system and the observer.

A reproducible demonstration gives useful evidence about a defined test. It does not by itself show that a system is secure under real-world conditions.

Agent Effect Check is:

- Not a penetration test.
- Not a comprehensive security audit.
- Not a formal verification or certification service.
- Not a guarantee that an AI agent cannot produce unauthorized effects.
- Not a replacement for your existing security controls.

Results are limited to the tested workflow, scenarios, instrumentation, and available evidence.

## Authorization and scope

Testing is performed only on systems you own or have explicitly authorized me in writing to test. Before work begins, we agree on the workflow, permitted actions, test environment, scope, and evidence required. I do not test a third party's system without permission.

## Contact

**Gokul Jayaprakash**

Email: gokuljayaprakashnair@gmail.com
