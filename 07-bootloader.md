# Step 7 - Bootloader (GRUB)

> GRUB is the bootloader that starts your Arch Linux system after the firmware hands over control.

---

## Install GRUB and EFI Boot Manager

```bash
pacman -S grub efibootmgr
```

---

## Install GRUB to EFI

```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```

---

## Generate GRUB Config

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

---

## Verify

You should see output like:
```
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-linux
Found initrd image: /boot/initramfs-linux.img
done
```

---

## Tips

- If `grub-install` fails, make sure `/boot` is mounted to the correct EFI partition
- The `--bootloader-id=GRUB` sets the name shown in your BIOS boot menu - you can change it
- Always run `grub-mkconfig` after any kernel or GRUB config changes

---

[Back - System Configuration](./06-system-config.md) | [Next - Services and Post-Install](./08-services-postinstall.md)
