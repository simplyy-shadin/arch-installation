# Arch Linux Issues and Fixes

> A collection of real-world issues encountered during and after Arch Linux installation - with working fixes.

---

## Table of Contents

1. [Brightness Stuck at Zero - AMD GPU](#1-brightness-stuck-at-zero---amd-gpu)
2. [SDDM Login Theme Not Changing](#2-sddm-login-theme-not-changing)
3. [Creating Bootable USB with PowerISO](#3-creating-bootable-usb-with-poweriso)
4. [Update Errors - Mirror Too Slow or SSL Errors](#4-update-errors---mirror-too-slow-or-ssl-errors)
5. [Boot Partition Full - Not Enough Free Disk Space](#5-boot-partition-full---not-enough-free-disk-space)

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

[Back to Main Guide](./README.md)
