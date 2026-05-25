# Step 2 - Connect to Internet

> Arch Linux installation requires an active internet connection to download packages.

---

## Option A - WiFi using iwctl

```bash
# Check network interfaces
ip link

# Start interactive wireless control tool
iwctl

# Inside iwctl prompt:
device list                              # list available WiFi devices
station wlan0 get-networks               # scan and show available networks
station wlan0 connect "YourWiFiName"     # connect (enter password when prompted)
exit                                     # exit iwctl
```

### Verify connection

```bash
ping -c 3 archlinux.org
```

---

## Option B - Ethernet

If you are using a wired connection, it should work automatically.
Just verify with:

```bash
ip link          # look for an interface like eth0 or enp3s0
ping -c 3 archlinux.org
```

---

## Tips

- If `wlan0` doesn't appear, your WiFi card may not be supported by the live ISO
- Try `iwctl device list` to find the correct device name (could be `wlan1` etc.)
- WiFi name is case-sensitive

---

[Back - Pre-Boot Setup](./01-pre-boot.md) | [Next - Disk Partitioning](./03-disk-partition.md)
