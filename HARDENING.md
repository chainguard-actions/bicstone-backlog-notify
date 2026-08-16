<!-- markdownlint-disable -->

# Hardening Report: bicstone--backlog-notify/v5.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **bicstone--backlog-notify/v5.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/test.yml references three Actions using mutable version tags instead of pinned full-length SHA digests. This exposes the workflow to supply-chain attacks if any of these tags are moved or compromised. Failing references: `actions/checkout@v4` (line 14), `actions/setup-node@v4` (line 15), `codecov/codecov-action@v4` (line 22). Each should be pinned to a full 40-character commit SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:15`
- `.github/workflows/test.yml:22`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level `permissions:` key and the only job (`Build`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or on the job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned all three action references in .github/workflows/test.yml to full commit SHAs: actions/checkout@v4 → 11d5960a326750d5838078e36cf38b85af677262, actions/setup-node@v4 → 49933ea5288caeca8642d1e84afbd3f7d6820020, codecov/codecov-action@v4 → b9fd7d16f6d7d1b5d2bec1a2887e65ceed900238. Added top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required permissions.

