# Local patches on OneCLI 1.45.0

This branch (`nanoclaw/1.45`) is upstream tag `v1.45.0` plus the patches below.
NanoClaw pins OneCLI 1.45 (`.claude/skills/add-onecli/versions.json`) by image
digest. This build is not upstream's, so it never reports a plain `1.45.N`: the
root `package.json` version, the git tag and the image tag are all
`1.45.N-nanoclaw.M` (tag `v1.45.N-nanoclaw.M`). Bump `M` for each release.

One commit per patch. To rebase onto a new base: `git rebase --onto <tag> v1.45.0`.

| # | Patch | Why |
|---|-------|-----|
| 1 | `google-docs`: request the `https://www.googleapis.com/auth/documents` scope | With only `drive.file` + `drive.readonly`, agents can read every doc but edit only docs OneCLI created; `batchUpdate` on a user's own doc fails with 403 PERMISSION_DENIED. Existing connections must reconnect to pick up the scope, and the scope must be added to the Google Cloud OAuth consent screen. Backport: upstream `main` already requests this scope for `google-docs`. |
| 2 | CI: `publish-nanoclaw.yml` publishes only `v*-nanoclaw.*` tags on `nanoclaw/1.45` that match `package.json`, one exact image tag, signed provenance, actions pinned by commit; `release.yml` removed | The fork must not publish 2.x code under its name or run upstream's release automation. Repo setting: disable upstream's `publish.yml` workflow (it still lives on `main`). |
| 3 | Version `1.45.0-nanoclaw.1` | `/v1/health` tells this build apart from upstream's 1.45.0. |
