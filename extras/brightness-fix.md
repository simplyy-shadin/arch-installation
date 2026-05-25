# AMD Brightness Fix

> If your AMD GPU brightness control is stuck at zero or not working after install,
> this fix resolves it by passing a kernel parameter via GRUB.

---

## The Problem

On some AMD laptops and desktops, the backlight brightness cannot be adjusted after boot.
This happens because the `amdgpu` driver doesn't automatically enable backlight control.

---

## The Fix

### Step 1 - Edit GRUB config

```bash
sudo vim /etc/default/grub
```

Find the line that starts with:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

Add `amdgpu.backlight=0` to it:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash amdgpu.backlight=0"
```

---

### Step 2 - Regenerate GRUB config

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

---

### Step 3 - Reboot

```bash
reboot
```

After reboot, your brightness controls should work correctly.

---

## Notes

- This fix is specifically for AMD GPUs with the `amdgpu` driver
- If you are using NVIDIA, this fix does not apply
- You can also try `acpi_backlight=native` if `amdgpu.backlight=0` does not work
- Always regenerate GRUB config after any changes to `/etc/default/grub`

---

[Back to Main Guide](../README.md)
