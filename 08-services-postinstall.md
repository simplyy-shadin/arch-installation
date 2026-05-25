# Step 8 - Services and Post-Install

> Enable essential services, reboot into your new system, then set up your environment.

---

## Enable Essential Services

```bash
sudo systemctl enable NetworkManager.service
sudo systemctl enable bluetooth.service
sudo systemctl enable sddm.service
```

---

## Exit Chroot and Reboot

```bash
exit           # exit arch-chroot
umount -R /mnt # unmount all partitions
reboot         # reboot into your new system
```

> Remove the USB drive when the machine restarts.

---

## Post-Install Setup

### Git Global Config

```bash
git config --global init.defaultBranch main
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

---

### Install paru (AUR Helper)

```bash
git clone https://aur.archlinux.org/paru-bin.git
cd paru-bin
makepkg -si
```

---

### Disable Fish Shell Greeting

```bash
nano ~/.config/fish/config.fish
```

Add this line:
```
set fish_greeting
```

---

## Services Reference

| Service | What it does |
|---------|--------------|
| `NetworkManager` | Manages WiFi and Ethernet connections |
| `bluetooth` | Enables Bluetooth support |
| `sddm` | Display manager - shows the login screen |

---

## You are done!

Your Arch Linux system is fully installed and configured.
Check out the package lists to install your desktop environment:

- [KDE Plasma Packages](./packages/plasma-packages.md)
- [Hyprland Packages](./packages/hyprland-packages.md)

And extras:
- [AMD Brightness Fix](./extras/brightness-fix.md)
