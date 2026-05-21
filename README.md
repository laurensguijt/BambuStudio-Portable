# Bambu Studio Portable

**Unofficial portable fork of [Bambu Studio](https://github.com/bambulab/BambuStudio).**

This repository builds a portable edition that stores all user data in a `portable_data` folder next to the application. That makes it suitable for cloud folders such as **OneDrive**, **Nextcloud**, **Google Drive**, and **Dropbox** — move or sync the whole folder without sharing settings with a normal installed Bambu Studio.

> **Note:** Do not open the same portable folder on two PCs at the same time. Wait for cloud sync to finish before launching on another computer.

## Download

Prebuilt Windows, macOS, and Linux portable releases:

**[Releases on this fork](https://github.com/laurensguijt/BambuStudio/releases)**

## Documentation

| Topic | Link |
|-------|------|
| Portable usage & migration | [PORTABLE.md](PORTABLE.md) |
| Automated releases | [RELEASE_BUILD.md](RELEASE_BUILD.md) |
| Upstream sync | [UPSTREAM_SYNC.md](UPSTREAM_SYNC.md) |

## Support

- **Bambu Studio bugs/features:** [bambulab/BambuStudio issues](https://github.com/bambulab/BambuStudio/issues)
- **Portable build/sync issues:** [issues on this fork](https://github.com/laurensguijt/BambuStudio/issues)

---

![image](https://user-images.githubusercontent.com/106916061/179006347-497d24c0-9bd6-45b7-8c49-d5cc8ecfe5d7.png)
# About Bambu Studio
Bambu Studio is a cutting-edge, feature-rich slicing software.  
It contains project-based workflows, systematically optimized slicing algorithms, and an easy-to-use graphic interface, bringing users an incredibly smooth printing experience.

Official prebuilt releases from Bambu Lab are available through the [upstream releases page](https://github.com/bambulab/BambuStudio/releases/).

Bambu Studio is based on [PrusaSlicer](https://github.com/prusa3d/PrusaSlicer) by Prusa Research, which is from [Slic3r](https://github.com/Slic3r/Slic3r) by Alessandro Ranellucci and the RepRap community.

See the [wiki](https://github.com/bambulab/BambuStudio/wiki) and the [documentation directory](https://github.com/bambulab/BambuStudio/tree/master/doc) for more information.

# What are Bambu Studio's main features?
Key features are:
- Basic slicing features & GCode viewer
- Multiple plates management
- Remote control & monitoring
- Auto-arrange objects
- Auto-orient objects
- Hybrid/Tree/Normal support types, Customized support
- multi-material printing and rich painting tools
- multi-platform (Win/Mac/Linux) support
- Global/Object/Part level slicing parameters

Other major features are:
- Advanced cooling logic controlling fan speed and dynamic print speed
- Auto brim according to mechanical analysis
- Support arc path(G2/G3)
- Support STEP format
- Assembly & explosion view
- Flushing transition-filament into infill/object during filament change

# How to compile
Following platforms are currently supported to compile:
- Windows 64-bit, [Compile Guide](https://github.com/bambulab/BambuStudio/wiki/Windows-Compile-Guide)
- Mac 64-bit, [Compile Guide](https://github.com/bambulab/BambuStudio/wiki/Mac-Compile-Guide)
- Linux, [Compile Guide](https://github.com/bambulab/BambuStudio/wiki/Linux-Compile-Guide)
  - currently we only provide linux appimages on [github releases](https://github.com/bambulab/BambuStudio/releases) for Ubuntu/Fedora, and a [flathub version](https://flathub.org/apps/com.bambulab.BambuStudio) can be used for all the linux platforms

# Report issue
For bugs in Bambu Studio itself, use the [upstream issue tracker](https://github.com/bambulab/BambuStudio/issues).

For problems specific to this portable fork (builds, sync, cloud/portable data), use the [issue tracker on this repository](https://github.com/laurensguijt/BambuStudio/issues).

# License
Bambu Studio is licensed under the GNU Affero General Public License, version 3. Bambu Studio is based on PrusaSlicer by PrusaResearch.

PrusaSlicer is licensed under the GNU Affero General Public License, version 3. PrusaSlicer is owned by Prusa Research. PrusaSlicer is originally based on Slic3r by Alessandro Ranellucci.

Slic3r is licensed under the GNU Affero General Public License, version 3. Slic3r was created by Alessandro Ranellucci with the help of many other contributors.

The GNU Affero General Public License, version 3 ensures that if you use any part of this software in any way (even behind a web server), your software must be released under the same license.

The bambu networking plugin is based on non-free libraries. It is optional to the Bambu Studio and provides extended networking functionalities for users.
By default, after installing Bambu Studio without the networking plugin, you can initiate printing through the SD card after slicing is completed.

