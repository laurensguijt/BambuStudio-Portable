# Bambu Studio Portable

This fork provides an unofficial **portable** edition of [Bambu Studio](https://github.com/bambulab/BambuStudio). Builds use the same dependencies, assets, translations, and packaging layout as upstream, with portable-specific changes isolated on the `portable` branch.

## What is different?

- The application title and About dialog show **Bambu Studio Portable**.
- User settings, profiles, cache, plugins, and logs are stored in a `portable_data` folder next to the application.
- Portable builds do not use the normal per-user install data folders, so they can run alongside an installed copy of Bambu Studio.

## Data location

On startup, the app resolves the application directory and stores data in `portable_data`:

### Windows

```text
BambuStudioPortable/
|-- bambu-studio.exe
|-- BambuStudio.dll
|-- resources/
`-- portable_data/
    |-- BambuStudio.conf
    |-- cache/
    |   |-- temp/
    |   `-- WebView2Cache/
    |-- log/
    |-- plugins/
    |-- profiles/
    |-- user/
    |-- system/
    |-- vendor/
    `-- ota/
```

### Linux (AppImage or tarball layout)

```text
BambuStudio/
|-- BambuStudio_ubu64.AppImage   (or bin/bambu-studio)
|-- resources/
`-- portable_data/
    `-- ...
```

For AppImage builds, `portable_data` is created next to the AppImage file.

### macOS

```text
ReleaseFolder/
|-- BambuStudio.app
`-- portable_data/
    `-- ...
```

## Migrate existing settings

Close Bambu Studio before copying files.

1. Start the portable build once, then close it to create `portable_data`.
2. Copy the contents of your normal Bambu Studio data folder into `portable_data`.

Windows source folder:

```text
%APPDATA%\BambuStudio
```

Optional WebView2 login cache from:

```text
%LOCALAPPDATA%\BambuStudio\WebView2Cache
```

Copy that into:

```text
portable_data\cache\WebView2Cache
```

## Cloud sync notes

Portable mode works with OneDrive, Nextcloud, Google Drive, Dropbox, and similar services. Avoid running the same portable folder on two PCs at the same time. Let sync finish before opening Bambu Studio on another machine.

The `cache` and `log` folders change frequently. Excluding logs from sync is usually safe. Excluding `cache\WebView2Cache` may require signing in again on each PC.

## Branch layout

| Branch | Purpose |
|--------|---------|
| `master` | Tracks upstream Bambu Studio without portable changes |
| `portable` | Upstream plus portable build flag, runtime behavior, CI, and docs |

## Build locally

Enable portable mode with CMake:

```bash
cmake -S . -B build -DSLIC3R_PORTABLE=1 ...
```

On Windows, after building, run the executable from its output folder. The first launch creates `portable_data` beside the binary.

See [RELEASE_BUILD.md](RELEASE_BUILD.md) for CI and release details.

## Related docs

- [UPSTREAM_SYNC.md](UPSTREAM_SYNC.md) — how upstream changes are merged
- [RELEASE_BUILD.md](RELEASE_BUILD.md) — automated portable releases
