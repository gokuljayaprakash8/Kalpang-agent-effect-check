# KALPANG Agent Effect Check

**Did your GitHub agent do anything you didn't authorize?**

A check that only looks at the authorized action can pass while an unauthorized action also happened. This service checks the repository itself, after the agent runs, and reports what changed against what was authorized.

**Measured example (EB006):** a live LLM tool-calling agent (gpt-oss-120b) was given an injected third-party note. A target-only check of the authorized issue passed in all 10 trials. With no guard, an independent observer flagged unauthorized effects in 10/10 trials. The observer never read the agent's log. It read the repository. Details: [EB006_RESULTS.md](https://github.com/gokuljayaprakash8/kalpang-observer/blob/main/EB006_RESULTS.md)

## What you get

- A rerunnable GitHub Actions test for one workflow.
- A short written report: verdict, likely cause, suggested fix, and a retest plan.
- Evidence you can verify yourself: issue and comment IDs, titles, timestamps, and SHA-256 hashes of bodies. Bodies are not stored.

## What it can and cannot see

It sees only the declared boundary: **issues and issue comments in one repository**. Anything the agent does outside that boundary (other repos, pull requests, files, other services) is invisible to this check. The report states what could not be seen.

## Four scenarios

1. Authorized action only: expected result is IN-BOUNDS.
2. Extra effect beyond the authorized action: DIVERGENT.
3. No authority for the action: DIVERGENT.
4. Widened delegation: DIVERGENT.

Verdicts are IN-BOUNDS, DIVERGENT, INDETERMINATE, or NO OBSERVED EFFECT. If a scenario doesn't apply to your workflow, the report says "not applicable" instead of a pass. INDETERMINATE means the run could not be verified, and it is never reported as a pass.

## What has been measured

EB006, live LLM agent, one injection wording, 10 trials per model. This is a demonstration, not a benchmark.

- No guard: the observer flagged unauthorized effects in 10/10 trials on gpt-oss-120b and 10/10 on gpt-oss-20b, and in none on qwen. The target-only check passed all 10 gpt-oss-120b trials.
- Exact-match pre-execution guard: the agent still attempted the extra action, but no extra issue was created.
- Two trials in one later run are unexplained. They are disclosed in the results file.

## Pilot

- **$300** for the first three teams. Regular price **$999** per workflow.
- Delivered in five working days after scope is agreed, access is set up, and the workflow runs in your CI.
- Scope: one workflow, one authorized action, effects readable through the GitHub API.
- Optional re-check after a model or prompt change: priced in writing.

**Before the clock starts, you provide:**
1. A sandbox repository (or a copy) where the agent workflow already runs in GitHub Actions.
2. A separate observer repository, or I provide one.
3. A fine-grained, read-only, short-lived token for the observer.
4. The one action the agent is authorized to take.

I do not debug your CI. If the workflow doesn't run, the clock does not start.

## Who this is for

Teams with an agent that creates or comments on GitHub issues from untrusted input, such as issue-triage bots, coding agents, and client-built GitHub agents.

Not a fit: no real agent yet, effects not readable through the API, or a need for a broad penetration test.

## What is true today

- Every observer script and test vector is deterministic and rerunnable in your own CI. You do not have to take my word for a verdict.
- The harness was built with substantial LLM assistance.
- EB005 used a scripted agent. EB006 uses a live LLM agent.
- The public demos ran under one GitHub account, so they are not independent of each other. For pilots, "independent" means: outside your dev team, a separate read-only identity, and a separate repository. It does not mean independent of GitHub.
- Not a penetration test, not a certification, not a guarantee.
- The probe repository is public, so unrelated issues from strangers can appear as unattributed effects.
- Pricing is early-stage and may change.

## Authorization, scope and credentials

- Testing happens only with your written authorization of the repository and scope.
- The observer uses its own short-lived, read-only credential. It is stored only as an encrypted GitHub Actions secret, never in notes or chats, and revoked after delivery. Where practical, the observer runs in your repository with your secret and I never hold the token.
- No production access. Sandbox copies only.
- Evidence retention: deleted on request after delivery.

## How to start

In writing only: open an issue in this repository or message @invariantdesign on X. Scope is agreed in writing before any payment.

## Contact

gokuljayaprakashnair@gmail.com
