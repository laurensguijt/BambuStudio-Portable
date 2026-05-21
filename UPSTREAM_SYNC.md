# Upstream Sync

This document describes how the `main` branch stays aligned with [bambulab/BambuStudio](https://github.com/bambulab/BambuStudio).

## Branch policy

- This fork uses one branch: **`main`**.
- `main` contains upstream Bambu Studio plus the portable-specific changes.
- Automated sync merges `upstream/master` into `main`.

## Automated workflow

Workflow: [`.github/workflows/sync_upstream.yml`](.github/workflows/sync_upstream.yml)

Triggers:

- Daily at 06:00 UTC
- Manual **Run workflow** from the Actions tab

Steps:

1. Check out the `main` branch.
2. Fetch `upstream/master` and upstream release tags.
3. Merge `upstream/master` into `main`.
4. Push the updated `main` branch on success.
5. If a new upstream release tag has no matching portable release (`vX.Y.Z-portable.1`), dispatch the portable build workflow.

## Conflict handling

If the merge fails:

- The workflow stops before pushing.
- A GitHub issue is opened.
- No release build is triggered until the conflict is resolved manually.

### Resolve a conflict locally

```bash
git fetch origin
git fetch upstream
git checkout main
git merge upstream/master
# resolve conflicts in your editor
git add .
git commit
git push origin main
```

After pushing, you can manually run **Sync upstream** or wait for the next scheduled sync.

## Detecting new upstream releases

The workflow uses the latest upstream GitHub release tag when available. If no release exists, it falls back to the newest `v*` tag in the upstream repository.

A portable release is created only when the tag `vX.Y.Z-portable.1` does not already exist on the fork.

To publish an additional rebuild for the same upstream version, run **Build Portable Release** manually with a higher `portable_revision` (for example `2` creates `vX.Y.Z-portable.2`).

## Remotes

```bash
git remote add upstream https://github.com/bambulab/BambuStudio.git
git fetch upstream
```

Expected remotes:

| Remote | URL |
|--------|-----|
| `origin` | `https://github.com/laurensguijt/BambuStudio.git` |
| `upstream` | `https://github.com/bambulab/BambuStudio.git` |
