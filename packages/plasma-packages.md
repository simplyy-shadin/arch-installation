# KDE Plasma Package List

> Full package list for a KDE Plasma desktop setup on Arch Linux.
> Install with pacstrap or pacman after chroot.

---

## Install Command

```bash
pacman -S sddm sddm-kcm plasma-desktop networkmanager plasma-nm plasma-pa \
bluez-utils bluedevil power-profiles-daemon plasma-systemmonitor plymouth \
kate nano konsole dolphin kscreen kwallet-pam git reflector \
gwenview kimageformats ark unrar p7zip okular spectacle kamoso \
fish zsh bash mesa nvidia nvidia-utils nvidia-settings grub efibootmgr
```

---

## Package Descriptions

### System Essentials

| Package | Description |
|---------|-------------|
| `base` | Minimal package group for a working Arch install |
| `base-devel` | Essential dev tools - gcc, make, etc. |
| `linux` | The Linux kernel |
| `linux-firmware` | Firmware for WiFi cards, GPUs, etc. |
| `amd-ucode` / `intel-ucode` | CPU microcode updates - improves stability |

### Graphics and Display

| Package | Description |
|---------|-------------|
| `mesa` | Open-source OpenGL implementation for 3D rendering |
| `nvidia` | NVIDIA proprietary drivers for modern GPUs |
| `nvidia-utils` | Essential utilities for NVIDIA drivers |
| `nvidia-settings` | GUI tool to configure NVIDIA GPU settings |
| `grub` | Bootloader that starts your OS |
| `efibootmgr` | Manages EFI boot entries on UEFI systems |

### Plasma Desktop Environment

| Package | Description |
|---------|-------------|
| `sddm` | Simple Desktop Display Manager - login screen for Plasma |
| `sddm-kcm` | KDE config module to customize SDDM |
| `plasma-desktop` | The KDE Plasma desktop environment |
| `networkmanager` | Network connection manager for WiFi/Ethernet/VPN |
| `plasma-nm` | KDE applet for managing network connections |
| `plasma-pa` | Volume control applet for Plasma |
| `bluez-utils` | Utilities for Bluetooth support |
| `bluedevil` | KDE Plasma tool to manage Bluetooth devices |
| `power-profiles-daemon` | Manages power-saving profiles |
| `plasma-systemmonitor` | Monitor CPU, RAM and system performance |
| `plymouth` | Animated loading/splash screen |

### Productivity and Utilities

| Package | Description |
|---------|-------------|
| `kate` | Powerful KDE text editor |
| `nano` | Lightweight command-line text editor |
| `konsole` | Default terminal emulator for KDE |
| `dolphin` | KDE file manager |
| `kscreen` | Manage multiple displays in KDE |
| `kwallet-pam` | Integrates KDE Wallet with system authentication |
| `git` | Distributed version control system |
| `reflector` | Auto-updates mirrorlist for faster downloads |

### Multimedia and File Management

| Package | Description |
|---------|-------------|
| `gwenview` | KDE image viewer |
| `kimageformats` | Adds extra image format support in KDE apps |
| `ark` | Tool for managing compressed files - zip, tar, etc. |
| `unrar` | Utility to extract .rar files |
| `p7zip` | Tool to manage .7z archives |
| `okular` | Document viewer for PDFs and eBooks |
| `spectacle` | Screenshot tool for KDE |
| `kamoso` | Webcam app for photos and videos |

### Shells

| Package | Description |
|---------|-------------|
| `fish` | User-friendly shell with autosuggestions |
| `zsh` | Powerful shell - great for customization |
| `bash` | Default shell for most Linux distributions |
