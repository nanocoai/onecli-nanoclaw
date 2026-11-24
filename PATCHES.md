# Local patches on OneCLI 1.45.0

This branch (`nanoclaw/1.45`) is upstream tag `v1.45.0` plus the patches below.
NanoClaw pins OneCLI 1.45 (`.claude/skills/add-onecli/versions.json`) and its
install check (`check-grants-gateway.sh`) accepts only a plain `1.45.N`
version, so keep the root `package.json` version in that form.

One commit per patch. To rebase onto a new base: `git rebase --onto <tag> v1.45.0`.

| # | Patch | Why |
|---|-------|-----|
| 1 | `google-docs`: request the `https://www.googleapis.com/auth/documents` scope | With only `drive.file` + `drive.readonly`, agents can read every doc but edit only docs OneCLI created; `batchUpdate` on a user's own doc fails with 403 PERMISSION_DENIED. Existing connections must reconnect to pick up the scope, and the scope must be added to the Google Cloud OAuth consent screen. Backport: upstream `main` already requests this scope for `google-docs`. |
