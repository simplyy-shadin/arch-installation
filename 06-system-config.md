# Step 6 - System Configuration

> Configure your new Arch Linux system - timezone, locale, hostname, user account.
> Run all commands inside `arch-chroot /mnt`.

---

## 1. Set Timezone

```bash
ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime
hwclock --systohc
```

> Replace `Asia/Kolkata` with your timezone. Browse available timezones:
> ```bash
> ls /usr/share/zoneinfo/
> ```

---

## 2. Localization

```bash
nano /etc/locale.gen
```

Uncomment your locale - e.g. `en_US.UTF-8 UTF-8`

```bash
locale-gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```

---

## 3. Set Hostname

```bash
echo "archbox" > /etc/hostname
```

> Replace `archbox` with whatever you want to name your machine.

---

## 4. Set Root Password

```bash
passwd
```

Enter and confirm your root password.

---

## 5. Create a User Account

```bash
useradd -m -G wheel -s /bin/bash shadin
passwd shadin
```

> Replace `shadin` with your username. Use **small letters only**.

### Give user sudo access

```bash
EDITOR=nano visudo
```

Uncomment this line:
```
%wheel ALL=(ALL:ALL) ALL
```

---

## Summary of Config Files Changed

| File | What it does |
|------|--------------|
| `/etc/localtime` | Sets the system timezone |
| `/etc/locale.gen` | Defines available locales |
| `/etc/locale.conf` | Sets the active locale |
| `/etc/hostname` | Sets the machine hostname |

---

[Back - Base Installation](./05-base-install.md) | [Next - Bootloader](./07-bootloader.md)
