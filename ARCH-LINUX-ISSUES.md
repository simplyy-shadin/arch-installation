# Arch Linux Issues and Fixes

> A collection of real-world issues encountered during and after Arch Linux installation - with working fixes.

---

## Table of Contents

1. [Brightness Stuck at Zero - AMD GPU](#1-brightness-stuck-at-zero---amd-gpu)
2. [SDDM Login Theme Not Changing](#2-sddm-login-theme-not-changing)
3. [Creating Bootable USB with PowerISO](#3-creating-bootable-usb-with-poweriso)
4. [Update Errors - Mirror Too Slow or SSL Errors](#4-update-errors---mirror-too-slow-or-ssl-errors)
5. [Boot Partition Full - Not Enough Free Disk Space](#5-boot-partition-full---not-enough-free-disk-space)
6. [No Sound After Install - PipeWire Not Working](#6-no-sound-after-install---pipewire-not-working)
7. [Pacman Keyring Errors - Invalid Signature](#7-pacman-keyring-errors---invalid-signature)
8. [Black Screen After Login - SDDM Loads but Desktop Doesn't Start](#8-black-screen-after-login---sddm-loads-but-desktop-doesnt-start)
9. [WiFi Not Connecting After Reboot - NetworkManager Issue](#9-wifi-not-connecting-after-reboot---networkmanager-issue)
10. [sudo: Command Not Found for Your User](#10-sudo-command-not-found-for-your-user)
11. [pacman -Syu Fails - Database Locked](#11-pacman--syu-fails---database-locked)
12. [Clock is Wrong - Time Sync Issue](#12-clock-is-wrong---time-sync-issue)

---

## 1. Brightness Stuck at Zero - AMD GPU

**Problem:** Screen brightness cannot be adjusted after AMD GPU install.

**Fix:**

### Step 1 - Edit GRUB config

```bash
sudo vim /etc/default/grub
```

Find this line:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

Add `amdgpu.backlight=0` to it:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash amdgpu.backlight=0"
```

### Step 2 - Regenerate GRUB config

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

### Step 3 - Reboot

```bash
reboot
```

---

## 2. SDDM Login Theme Not Changing

**Problem:** SDDM display manager is not applying the selected theme after changing it.

**Fix:** Edit the SDDM config file directly.

```bash
sudo vim /etc/sddm.conf.d/the_hyde_project.conf
```

Change the theme value to:
```
Current=Corners
```

Save and restart SDDM:
```bash
sudo systemctl restart sddm
```

---

## 3. Creating Bootable USB with PowerISO

**Steps:**

1. Open PowerISO
2. Select the **USB** option (not CD/DVD)
3. Select the Arch Linux ISO image
4. Choose type: **UEFI only**
5. Start burning

> Make sure to select UEFI only - not legacy/BIOS mode - for modern systems.

---

## 4. Update Errors - Mirror Too Slow or SSL Errors

**Problem:** `sudo pacman -Syu` fails with errors like:

```
error: failed retrieving file 'libreoffice-fresh-25.8.2-4-x86_64.pkg.tar.zst'
from in.arch.niranjan.co : OpenSSL SSL_read: OpenSSL/3.5.2:
error:0A000126:SSL routines::unexpected eof while reading, errno 0

error: failed retrieving file 'alsa-lib-1.2.14-2-x86_64.pkg.tar.zst'
from in.arch.niranjan.co : Operation too slow.
Less than 1 bytes/sec transferred the last 10 seconds

warning: too many errors from in.arch.niranjan.co, skipping for the remainder of this transaction
```

**Cause:** The mirror `in.arch.niranjan.co` is slow or having SSL issues.

**Fix:** Update your mirrorlist to use faster/working mirrors.

```bash
sudo reflector --country India --latest 10 --sort rate --save /etc/pacman.d/mirrorlist
```

Then retry the update:
```bash
sudo pacman -Syu
```

> If reflector is not installed: `sudo pacman -S reflector`

**Alternative manual fix:** Boot into a live USB, mount your partitions, and use pacstrap to re-download pacman:

```bash
sudo pacman -S arch-install-scripts
lsblk
# mount your partitions
pacstrap -K /mnt pacman
```

---

## 5. Boot Partition Full - Not Enough Free Disk Space

**Problem:** `sudo pacman -Syu` fails with:

```
error: Partition /boot too full: 4906 blocks needed, 0 blocks free
error: not enough free disk space
error: failed to commit transaction (not enough free disk space)
Errors occurred, no packages were upgraded.
```

**Cause:** The `/boot` EFI partition is completely full - no space left for new kernel files.

**Fix:**

### Step 1 - Install arch-install-scripts

```bash
sudo pacman -S arch-install-scripts
```

### Step 2 - Check disk layout

```bash
lsblk
```

### Step 3 - Unmount and reformat the boot partition

> Warning: This wipes your EFI partition. Make sure you know your partition names from `lsblk`.

```bash
sudo umount /boot
sudo mkfs.fat -F 32 /dev/nvme0n1p1
```

### Step 4 - Rebuild boot setup

Run all of these in sequence:

```bash
sudo rm -rf /boot
sudo mkdir /boot
sudo mkdir /boot/efi
sudo mount /dev/nvme0n1p1 /boot/efi
sudo rm /etc/fstab
sudo genfstab -U / >> /etc/fstab
sudo pacman -S linux
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB
```

### Step 5 - Regenerate GRUB config

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

### Step 6 - Reboot

```bash
reboot
```

---

---

## 6. No Sound After Install - PipeWire Not Working

**Problem:** Audio is completely silent after install even though speakers/headphones are connected.

**Cause:** PipeWire or WirePlumber service is not running.

**Fix:**

### Step 1 - Install audio packages if missing

```bash
sudo pacman -S pipewire pipewire-alsa pipewire-pulse pipewire-jack wireplumber
```

### Step 2 - Enable and start the services

```bash
systemctl --user enable pipewire pipewire-pulse wireplumber
systemctl --user start pipewire pipewire-pulse wireplumber
```

### Step 3 - Check status

```bash
systemctl --user status pipewire
```

### Step 4 - Reboot

```bash
reboot
```

> If sound still doesn't work, try `pavucontrol` to check if output device is muted or set to wrong sink.

---

## 7. Pacman Keyring Errors - Invalid Signature

**Problem:** Packages fail to install with errors like:

```
error: key "XXXXXXXXXXXXXXXX" could not be looked up remotely
error: required key missing from keyring
error: failed to commit transaction (invalid or corrupted package (PGP signature))
```

**Cause:** The pacman keyring is outdated or corrupted.

**Fix:**

```bash
sudo pacman-key --init
sudo pacman-key --populate archlinux
sudo pacman -Sy archlinux-keyring
sudo pacman -Syu
```

> If it still fails, remove the keyring and reinitialize:

```bash
sudo rm -rf /etc/pacman.d/gnupg
sudo pacman-key --init
sudo pacman-key --populate archlinux
```

---

## 8. Black Screen After Login - SDDM Loads but Desktop Doesn't Start

**Problem:** SDDM login screen appears, you enter credentials, then you get a black screen with a cursor.

**Cause:** Usually a missing display server, wrong session set in SDDM, or GPU driver issue.

**Fix - Check which session is selected:**

At SDDM login screen, look for a session selector (usually bottom left). Make sure it says **Plasma** or **Hyprland** - not a blank or wrong entry.

**Fix - Reinstall plasma/hyprland:**

```bash
sudo pacman -S plasma-desktop
# or for Hyprland
sudo pacman -S hyprland
```

**Fix - Check Xorg/Wayland logs:**

```bash
journalctl -b -p err
```

**Fix - If NVIDIA GPU:**

```bash
sudo pacman -S nvidia nvidia-utils
sudo mkinitcpio -P
sudo grub-mkconfig -o /boot/grub/grub.cfg
reboot
```

---

## 9. WiFi Not Connecting After Reboot - NetworkManager Issue

**Problem:** WiFi worked during install but stops working after reboot into the installed system.

**Cause:** NetworkManager service is not enabled or iwd is conflicting with it.

**Fix - Enable NetworkManager:**

```bash
sudo systemctl enable --now NetworkManager
```

**Fix - Check status:**

```bash
sudo systemctl status NetworkManager
```

**Fix - If using iwd alongside NetworkManager (conflict):**

```bash
sudo systemctl disable iwd
sudo systemctl restart NetworkManager
```

**Fix - Connect manually via nmcli:**

```bash
nmcli device wifi list
nmcli device wifi connect "YourWiFiName" password "YourPassword"
```

---

## 10. sudo: Command Not Found for Your User

**Problem:** Running `sudo` gives:

```
shadin is not in the sudoers file. This incident will be reported.
```

**Cause:** Your user was not added to the `wheel` group or visudo was not configured.

**Fix - Switch to root and fix it:**

```bash
su -
EDITOR=nano visudo
```

Uncomment this line:
```
%wheel ALL=(ALL:ALL) ALL
```

Then add your user to the wheel group:
```bash
usermod -aG wheel shadin
```

Log out and back in - sudo will now work.

---

## 11. pacman -Syu Fails - Database Locked

**Problem:** Running `sudo pacman -Syu` shows:

```
error: failed to init transaction (unable to lock database)
error: could you be running two instances of pacman?
```

**Cause:** A previous pacman process crashed and left a lock file behind.

**Fix:**

```bash
sudo rm /var/lib/pacman/db.lck
sudo pacman -Syu
```

> Only do this if you are sure no other pacman process is running.

---

## 12. Clock is Wrong - Time Sync Issue

**Problem:** System clock shows wrong time after install or after switching between Windows and Arch (dual boot).

**Fix - Enable NTP time sync:**

```bash
sudo timedatectl set-ntp true
timedatectl status
```

**Fix - If dual booting with Windows (RTC clock conflict):**

Windows uses local time, Arch uses UTC by default. Fix by making Arch use local time:

```bash
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```

**Fix - Set correct timezone:**

```bash
sudo timedatectl set-timezone Asia/Kolkata
```

---

[Back to Main Guide](./README.md)

[Back to Main Guide](./README.md)
