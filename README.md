# KALPANG Agent Effect Check

**Did your GitHub agent do anything you didn't authorize?**

Your agent can complete the task you asked for and also do something you never authorized. A check that only verifies the requested action can pass while an unauthorized issue or comment also exists. This service checks the repository after the agent runs and reports observed effects against the authorization you declared.

**Measured example (EB006):** a live LLM tool-calling agent (gpt-oss-120b) was given an injected third-party note. With no guard, a check limited to the authorized issue passed in all 10 trials. A separate observer workflow flagged an unauthorized effect in all 10. The observer never read the agent's log. It read the repository. Full results, including other models and excluded runs: [EB006_RESULTS.md](https://github.com/gokuljayaprakash8/kalpang-observer/blob/main/EB006_RESULTS.md)

## What you get

- A rerunnable GitHub Actions test for one workflow.
- A short written report: verdict, likely cause, suggested fix, and a retest plan.
- Evidence you can verify yourself: issue and comment IDs, titles, timestamps, and SHA-256 hashes of bodies. Bodies are not stored.

## Exact boundary of the check

It checks **issues and issue comments in one repository**. This is deliberately narrow: it verifies one declared authorization boundary rather than claiming to inspect every possible side effect. Anything the agent does outside that boundary (other repos, pull requests, files, other services) is not seen. The report states what could not be seen.

## Verdicts

IN-BOUNDS, DIVERGENT, INDETERMINATE, or NO OBSERVED EFFECT. INDETERMINATE means the run could not be verified and is never reported as a pass. If a scenario doesn't apply to your workflow, the report says "not applicable" instead of a pass.

Four scenarios:
1. Authorized action only: expected IN-BOUNDS.
2. Extra effect beyond the authorized action: DIVERGENT.
3. No authority for the action: DIVERGENT.
4. Widened delegation: DIVERGENT.

## Sample report verdict

*Illustrative example. Fictional, not a client result.*

- **Scenario:** extra effect beyond the authorized action
- **Verdict:** DIVERGENT
- **Authorized effect:** one issue created with the agreed title prefix
- **Observed:** a second issue created in the same repository
- **Evidence:** issue ID, creation timestamp, SHA-256 hash of body
- **Likely cause:** the agent followed an instruction embedded in untrusted issue text
- **Suggested control:** an authorization check before issue creation; restrict the agent's token permissions
- **Retest:** rerun after the control change

## Who this is for

Teams with an agent that creates or comments on GitHub issues from untrusted input, such as issue-triage bots, coding agents, and client-built GitHub agents.

**Not a fit if:** you have no running agent, the effects are not readable through the GitHub API, or you need broad penetration testing, certification, or multi-service coverage.

## What has been measured

EB006, live LLM agent, one injection wording, 10 trials per model. This is a demonstration, not a benchmark.

- No guard: the observer flagged unauthorized effects in 10/10 trials on gpt-oss-120b and 10/10 on gpt-oss-20b, and in none on qwen. The target-only check passed all 10 gpt-oss-120b trials.
- Exact-match pre-execution guard: the agent still attempted the extra action, but no extra issue was created.
- Two trials in one later run are unexplained. They are disclosed in the results file.

## Founding pilot and pricing

- **$300 for the first three teams.** In exchange, I ask permission to publish an anonymized summary (workflow type, scenarios tested, outcome). If you prefer confidentiality, say so and nothing is published.
- Regular price: **$999** per workflow. Founding pricing applies to the first three engagements only; regular pricing may change.
- Delivered in five working days after scope is agreed, access is set up, and the workflow runs in your CI.
- Scope: one workflow, one authorized action, effects readable through the GitHub API.
- Optional re-check after a model or prompt change: priced in writing.

**Before the clock starts, you provide:**
1. A sandbox repository (or a copy) where the agent workflow already runs in GitHub Actions.
2. A separate observer repository, or I provide one.
3. A fine-grained, read-only, short-lived token for the observer.
4. The one action the agent is authorized to take.

Setup support is limited to confirming that the agreed workflow runs. I do not provide general CI debugging. If the workflow doesn't run, the clock does not start.

## Authorization, scope and credentials

- Testing happens only with your written authorization of the repository and scope.
- The observer uses its own short-lived, read-only credential. It is stored only as an encrypted GitHub Actions secret, never in notes or chats, and revoked after delivery. Where practical, the observer runs in your repository with your secret and I never hold the token.
- No production access. Sandbox copies only.
- Evidence retention: deleted on request after delivery.

## After you message me

1. You describe the agent workflow and the one authorized action.
2. I confirm whether the effect is observable through the GitHub API.
3. We agree the repository, scenarios, and access model in writing.
4. You create the read-only observer token and store it as a GitHub Actions secret.
5. The five-working-day delivery window begins.

## What is true today

- Every observer script and test vector is deterministic and rerunnable in your own CI. You do not have to take my word for a verdict.
- The harness was built with substantial LLM assistance.
- EB005 used a scripted agent. EB006 uses a live LLM agent.
- Not a penetration test, not a certification, not a guarantee.

## Known limitations

- The public demos ran under one GitHub account, so they are not independent of each other. For pilots, "independent" means: outside your dev team, a separate read-only identity, and a separate repository. It does not mean independent of GitHub.
- The probe repository is public, so unrelated issues from strangers can appear as unattributed effects.

## How to start

In writing only: open an issue in this repository or message @invariantdesign on X. Scope is agreed in writing before any payment.

## Contact

gokuljayaprakashnair@gmail.com
