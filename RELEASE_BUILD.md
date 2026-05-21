# Portable Release Build

This document describes how automated portable releases are built and published on the fork.

## Workflows

| Workflow | Purpose |
|----------|---------|
| [`sync_upstream.yml`](.github/workflows/sync_upstream.yml) | Merge upstream into `portable` and trigger builds for new upstream releases |
| [`build_portable.yml`](.github/workflows/build_portable.yml) | Build and publish a portable GitHub release |
| [`build_all.yml`](.github/workflows/build_all.yml) | Upstream-style CI matrix (deps cache + app build) |

Portable releases reuse the upstream build matrix and packaging steps via [`build_check_cache.yml`](.github/workflows/build_check_cache.yml), [`build_deps.yml`](.github/workflows/build_deps.yml), and [`build_bambu.yml`](.github/workflows/build_bambu.yml) with `portable: true`.

## Build targets

Same OS and architecture matrix as upstream where possible:

| OS runner | Artifact |
|-----------|----------|
| `ubuntu-22.04` | AppImage |
| `ubuntu-24.04` | AppImage |
| `windows-latest` | ZIP portable folder |
| `macos-15-intel` | ZIP (x86_64) |
| `macos-15` | ZIP (Apple Silicon / universal build output) |

## Portable build flag

All portable CI builds pass:

```text
-DSLIC3R_PORTABLE=1
```

This enables:

- `SLIC3R_PORTABLE_BUILD` compile definition
- Application branding as **Bambu Studio Portable**
- Runtime storage in `portable_data` beside the application

Linux and macOS builds also honor the `EXTRA_CMAKE_ARGS` environment variable in `BuildLinux.sh` and `BuildMac.sh`.

## Release naming

| Item | Format | Example |
|------|--------|---------|
| Upstream tag | `vX.Y.Z` | `v1.3.1.1` |
| Portable tag | `vX.Y.Z-portable.N` | `v1.3.1.1-portable.1` |
| Release title | `Bambu Studio Portable vX.Y.Z` | `Bambu Studio Portable 1.3.1.1` |

## Package names

Portable artifacts use `_Portable` in the filename:

| Platform | Example |
|----------|---------|
| Windows | `BambuStudio_Portable_Windows_V02.07.00.55_portable.zip` |
| macOS | `BambuStudio_Portable_Mac_x86_64_V02.07.00.55.zip` |
| Linux | `BambuStudio_Portable_ubuntu-22.04_V02.07.00.55.AppImage` |

The version segment comes from `version.inc` in the synced `portable` branch.

## Release notes

Each portable release prepends:

```text
This is an unofficial portable build of Bambu Studio. User data is stored in the portable_data folder next to the application.
```

When available, the original upstream release notes for the matching tag are appended after a separator.

## Manual release

1. Open **Actions → Build Portable Release → Run workflow**.
2. Select branch `portable`.
3. Set `upstream_tag` to the upstream release tag (for example `v1.3.1.1`).
4. Set `portable_revision` if you need a rebuild (`1`, `2`, ...).

## Local Windows build

Example using the upstream Windows script with a prebuilt deps folder:

```bat
set PATH=C:\Strawberry\perl\bin;C:\Program Files\CMake\bin;%PATH%
build_win.bat -s app-dirty -d deps\build\out_deps -v 18 -r none
```

Configure with portable mode:

```bat
cmake -S . -B build -G "Visual Studio 18 2026" -A x64 -DSLIC3R_PORTABLE=1 -DBBL_RELEASE_TO_PUBLIC=1 -DBBL_INTERNAL_TESTING=0 -DCMAKE_PREFIX_PATH=deps\build\out_deps\usr\local
cmake --build build --config RelWithDebInfo --target install
```

Run the installed binary once to verify that `portable_data` is created next to the executable.

## Dependencies cache

Portable release builds use the same deps cache keys as upstream (`deps/**` hash). The first build on a runner may take longer while dependencies are compiled and cached.
