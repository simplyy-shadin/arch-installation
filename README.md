# Arch Linux Installation Guide

> A complete, battle-tested Arch Linux installation guide - from BIOS to a fully configured desktop.
> Supports both **KDE Plasma** and **Hyprland** setups.

![Arch Linux](https://img.shields.io/badge/Arch_Linux-1793D1?style=for-the-badge&logo=arch-linux&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Maintained-brightgreen?style=for-the-badge)

---

## Table of Contents

### Installation Steps

1. [Pre-Boot Setup](./01-pre-boot.md)
2. [Connect to Internet](./02-connect-internet.md)
3. [Disk Partitioning](./03-disk-partition.md)
4. [Format and Mount](./04-format-mount.md)
5. [Base Installation](./05-base-install.md)
6. [System Configuration](./06-system-config.md)
7. [Bootloader - GRUB](./07-bootloader.md)
8. [Services and Post-Install](./08-services-postinstall.md)

### Package Lists

- [KDE Plasma Packages](./packages/plasma-packages.md)
- [Hyprland Packages](./packages/hyprland-packages.md)

### Issues and Fixes

- [Arch Linux Issues and Fixes](./ARCH-LINUX-ISSUES.md)

---

## Prerequisites

- A USB drive with Arch Linux ISO burned
- A machine with UEFI firmware
- Internet connection (WiFi or Ethernet)
- Basic knowledge of terminal commands

---

## Quick Overview

| Step | What Happens |
|------|-------------|
| 1 | Boot from USB, disable Secure Boot |
| 2 | Connect to WiFi using iwctl |
| 3 | Partition disk - EFI + swap + root |
| 4 | Format and mount partitions |
| 5 | Install base system with pacstrap |
| 6 | Configure locale, timezone, hostname, user |
| 7 | Install and configure GRUB bootloader |
| 8 | Enable services - reboot into your new system |

---

## Desktop Environments Covered

### KDE Plasma
- Full Plasma desktop with SDDM login manager
- NetworkManager, Bluetooth, audio via PipeWire
- Essential KDE apps - Dolphin, Kate, Konsole, Gwenview

### Hyprland
- Wayland-native tiling compositor
- Waybar, Rofi, Dunst, Hyprpaper
- Full GPU support for NVIDIA + AMD

---

## Post-Install Highlights

- AUR helper setup using **paru**
- Fish shell with greeting disabled
- Git global config
- AMD backlight fix via GRUB params

---

## Author

Made by **Shadin**

### Connect with the Author

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shadin-k-v-cybersecurity)
[![TryHackMe](https://img.shields.io/badge/TryHackMe-212C42?style=for-the-badge&logo=tryhackme&logoColor=white)](https://tryhackme.com/p/simplyy.hacker)
[![Medium](https://img.shields.io/badge/Medium-000000?style=for-the-badge&logo=medium&logoColor=white)](https://medium.com/@shdnkval)

- LinkedIn - https://www.linkedin.com/in/shadin-k-v-cybersecurity
- TryHackMe - https://tryhackme.com/p/simplyy.hacker
- Medium - https://medium.com/@shdnkval

---

> If this guide helped you, drop a star - it means a lot!
