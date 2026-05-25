# Step 1 - Pre-Boot Setup

> Before installing Arch Linux, you need to prepare your machine's firmware settings.

---

## Steps

### 1. Enter BIOS

- Restart your machine
- Press the BIOS key during boot (usually `Del`, `F2`, `F10` or `Esc` depending on your motherboard)

### 2. Disable Secure Boot

- Navigate to the **Security** or **Boot** tab in BIOS
- Find **Secure Boot** and set it to **Disabled**
- This is required - Arch Linux ISO will not boot with Secure Boot enabled

### 3. Boot from USB

- Save BIOS changes and restart
- Press the boot menu key (usually `F8`, `F11` or `F12`)
- Select your USB drive from the boot menu
- You should now be dropped into the Arch Linux live environment

---

## Tips

- Make sure your USB was flashed correctly using a tool like `dd`, Balena Etcher or Rufus
- If the USB doesn't show up in the boot menu, try a different USB port (prefer USB 2.0)
- Disable **Fast Boot** in BIOS if you can't see the boot menu

---

[Next - Connect to Internet](./02-connect-internet.md)
