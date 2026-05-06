# APM Governance — Rollout Notes

This repo hosts the org-wide APM trust seed:

- [`apm-policy.yml`](../apm-policy.yml) — auto-discovered by `apm install` and
  `apm audit --ci` for every repo in `DigitalInnovation`.
- [`.github/workflows/apm-audit.yml`](../.github/workflows/apm-audit.yml) — a
  reusable workflow consumer repos can call to run `apm audit --ci`.

## Rollout phase: WARN

`enforcement: warn` is set deliberately. The recommended APM rollout (per the
[Governance Guide](https://microsoft.github.io/apm/enterprise/governance-guide/),
§11) is:

1. Land the policy in `warn` mode. **(we are here)**
2. Wire `apm-audit.yml` into repos as a non-required check; review the audit log artifact
   uploaded by each run.
3. Burn down violations.
4. Flip `enforcement: block` and make the audit job a required status check.

Do not flip `enforcement: block` without principal-engineers sign-off.

## Trust boundary

This repo IS the trust boundary. Anyone who can push to `main` here can
loosen org-wide policy. CODEOWNERS + branch protection on `main` are
load-bearing — keep both strict.

## What is *not* covered

APM is an install-time gate. It does not constrain LLM choice, runtime, MCP
`command`/`args` content, or perform semantic prompt-injection review. See
governance guide §4 for the full out-of-scope list.
