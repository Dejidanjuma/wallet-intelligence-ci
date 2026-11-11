# Wallet Intelligence CI Controller

This public repository contains manually triggered/private-source CI workflows only. Wallet Intelligence application source remains in the private repository and is checked out into an ephemeral GitHub-hosted runner.

## Private source credential

1. Create a fine-grained personal access token restricted to the private `Dejidanjuma/wallet-intelligence` repository.
2. Grant **Contents: Read-only** only.
3. Store it as the repository Actions secret `WI_READONLY_TOKEN`.
4. Do not paste the token into chat, source, workflow inputs, issues, artifacts or logs.

The verifier uses `persist-credentials: false`, disables install lifecycle scripts, writes no source changes, uploads no private artifacts/caches, and prints only stage PASS/FAIL labels. It does not deploy or access production database/exchange credentials.

## Workflows and permission boundaries

- `private-source-ci.yml` is manually triggered or invoked by a repository-dispatch event. It checks out the requested private commit into a temporary runner and runs lint, typecheck, tests and build.
- `poll-private-source.yml` is separately manual-only. Its workflow-scoped `GITHUB_TOKEN` has `contents: write` solely to update `.ci/last-seen-private-sha` in this controller and dispatch the validation event. The private source PAT remains read-only. Do not copy the write permission into the verifier workflow.
- No workflow deploys, applies migrations, submits trades, signs wallets, or performs transfers.

## Run

Open Actions → Private Wallet Intelligence CI → Run workflow and select an exact commit SHA when possible. Review the commit SHA and every stage result. A passing build is not production approval.
