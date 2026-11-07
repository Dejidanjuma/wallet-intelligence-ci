# Wallet Intelligence CI Controller

This public repository contains only a manually triggered CI workflow. The Wallet Intelligence application source remains in the private repository and is checked out only into an ephemeral GitHub-hosted runner.

## One-time setup

1. Create a fine-grained personal access token restricted to the private `Dejidanjuma/wallet-intelligence` repository with **Contents: Read-only** only.
2. Add it here under **Settings → Secrets and variables → Actions → New repository secret**.
3. Name the secret exactly `WI_READONLY_TOKEN`.
4. Never paste the token into chat, source code, issues, or logs.

The workflow prints only stage PASS/FAIL labels. It does not upload artifacts or caches, and does not deploy or access production database/exchange credentials.

## Run

Open **Actions → Private Wallet Intelligence CI → Run workflow** and select the feature branch target configured in the workflow.

Do not add automatic push or pull-request triggers.
