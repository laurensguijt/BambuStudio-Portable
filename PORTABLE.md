# Portable Bambu Studio

This fork always runs in portable mode on Windows. User data is stored next to the executable instead of in the Windows user profile, so the folder can be moved or cloud-synced without sharing settings with a normal installed Bambu Studio.

## Data Location

On startup, Bambu Studio resolves the executable directory and uses `portable_data` beside it:

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

Most folders are created on demand. Existing Bambu Studio code still uses the normal `Slic3r::data_dir()` layout; this fork only changes that root directory to `portable_data`.

## Migrate Existing Settings

Close Bambu Studio before copying files.

1. Start this portable fork once, then close it. This creates `portable_data`.
2. Copy the contents of the normal data folder into `portable_data`.

For a normal public Windows build, the source folder is usually:

```text
%APPDATA%\BambuStudio
```

Copy items such as `BambuStudio.conf`, `user`, `system`, `vendor`, `plugins`, `ota`, `filament_inventory`, `hms`, `cameratools`, and any other folders you want to carry over.

Login/session data used by WebView2 is stored separately in normal installs:

```text
%LOCALAPPDATA%\BambuStudio\WebView2Cache
```

To migrate browser login state, copy that folder into:

```text
portable_data\cache\WebView2Cache
```

## Cloud Sync Notes

Portable mode is suitable for OneDrive, Nextcloud, Google Drive, Dropbox, and similar folders, but avoid running the same portable folder on two PCs at the same time. Let sync finish before opening Bambu Studio on another PC.

The `cache` and `log` folders can change often. Excluding logs from sync is usually safe. Excluding `cache\WebView2Cache` may require signing in again on each PC.

Some settings may still refer to external model files, removable drives, device names, or other machine-specific choices. Those paths are user choices and may not exist on another PC.
