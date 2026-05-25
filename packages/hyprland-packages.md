# Hyprland Package List

> Full package list for a Hyprland Wayland compositor setup on Arch Linux.
> This is a minimal but fully functional tiling window manager setup.

---

## Install Command (via pacstrap or pacman)

```bash
pacman -S base base-devel linux linux-firmware amd-ucode mesa nvidia nvidia-utils \
nvidia-settings grub efibootmgr plymouth sddm sddm-kcm \
hyprland hyprpaper hyprpicker hypridle hyprlock hyprcursor \
xdg-desktop-portal-hyprland hyprpolkitagent dunst \
pipewire wireplumber qt5-wayland qt6-wayland \
waybar rofi-wayland dolphin git reflector \
gwenview kimageformats ark unrar p7zip okular \
obs-studio firefox zsh kitty
```

> Use small letters for username (pls pls pls).

---

## Package Descriptions

### Core Hyprland

| Package | Description |
|---------|-------------|
| `hyprland` | Wayland-native dynamic tiling compositor |
| `hyprpaper` | Wallpaper utility for Hyprland |
| `hyprpicker` | Color picker for Hyprland |
| `hypridle` | Idle daemon - dims/locks screen after inactivity |
| `hyprlock` | Lock screen for Hyprland |
| `hyprcursor` | Custom cursor theme support for Hyprland |
| `xdg-desktop-portal-hyprland` | Screen sharing and portal support for Hyprland |
| `hyprpolkitagent` | Polkit authentication agent for Hyprland |

### Status Bar and Notifications

| Package | Description |
|---------|-------------|
| `waybar` | Highly customizable Wayland status bar |
| `dunst` | Lightweight notification daemon |
| `rofi-wayland` | App launcher and dmenu replacement for Wayland |

### Audio

| Package | Description |
|---------|-------------|
| `pipewire` | Modern audio/video server for Linux |
| `wireplumber` | Session/policy manager for PipeWire |

### Qt Wayland Support

| Package | Description |
|---------|-------------|
| `qt5-wayland` | Qt5 Wayland platform plugin |
| `qt6-wayland` | Qt6 Wayland platform plugin |

### Apps and Tools

| Package | Description |
|---------|-------------|
| `dolphin` | KDE file manager |
| `kitty` | Fast GPU-accelerated terminal emulator |
| `firefox` | Web browser |
| `obs-studio` | Screen recording and streaming |
| `git` | Version control |
| `reflector` | Auto-updates mirror list |
| `gwenview` | Image viewer |
| `ark` | Archive manager |
| `okular` | PDF and document viewer |

### Shell

| Package | Description |
|---------|-------------|
| `zsh` | Powerful and customizable shell |
