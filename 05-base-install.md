# Step 5 - Base Installation

> This step installs the Arch Linux base system onto your mounted partitions.

---

## Step 1 - Update Mirrorlist for Fastest Servers

```bash
reflector --country India --latest 10 --sort rate --save /etc/pacman.d/mirrorlist
```

> Change `India` to your country for best speeds.

---

## Step 2 - Install Base System

```bash
pacstrap /mnt base base-devel linux linux-firmware amd-ucode nano git networkmanager
```

> Replace `amd-ucode` with `intel-ucode` if you have an Intel CPU.

### What each package does

| Package | Purpose |
|---------|--------|
| `base` | Minimal Arch Linux base |
| `base-devel` | Build tools - gcc, make, etc. |
| `linux` | The Linux kernel |
| `linux-firmware` | Firmware for hardware - WiFi, GPU etc. |
| `amd-ucode` | AMD CPU microcode updates |
| `nano` | Terminal text editor |
| `git` | Version control |
| `networkmanager` | Network management daemon |

---

## Step 3 - Generate fstab

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

> This generates the filesystem table so your system knows where to mount partitions on boot.

Verify it looks correct:
```bash
cat /mnt/etc/fstab
```

---

## Step 4 - Chroot into the New System

```bash
arch-chroot /mnt
```

You are now inside your new Arch Linux installation.

---

## Step 5 - Set Default Shell (Optional)

```bash
# Set fish as default shell
chsh -s /usr/bin/fish
```

---

## Tips

- If `pacstrap` fails, check your internet connection first
- Always verify `fstab` after generating - a wrong fstab can break boot
- You can add more packages to the `pacstrap` command if needed

---

[Back - Format and Mount](./04-format-mount.md) | [Next - System Configuration](./06-system-config.md)
