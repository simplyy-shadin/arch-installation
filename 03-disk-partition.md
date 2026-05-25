# Step 3 - Disk Partitioning

> This step partitions your disk to make space for Arch Linux.
> We will create 3 partitions - EFI, Swap, and Root.

---

## Step 1 - List Available Disks

```bash
fdisk -l
```

Look for your target disk - usually `/dev/sda`, `/dev/nvme0n1`, or `/dev/vda`.

---

## Step 2 - Wipe Disk (Optional but Recommended for Fresh Install)

```bash
gdisk /dev/sdX    # replace sdX with your disk name
```

Inside gdisk:
```
x        # enter expert mode
z        # zap/wipe all partition data
y        # confirm wipe
y        # confirm MBR wipe
```

---

## Step 3 - Create Partitions with cfdisk

```bash
cfdisk /dev/sdX
```

- Select **GPT** as the partition type
- Create the following 3 partitions:

| Partition | Type | Size | Purpose |
|-----------|------|------|---------|
| /dev/sdX1 | EFI System | 512M | Boot partition |
| /dev/sdX2 | Linux swap | 4G - 8G | Swap space |
| /dev/sdX3 | Linux filesystem | Remaining | Root filesystem |

### Steps in cfdisk

1. Select **New** - input size (e.g. `512M`)
2. Select the correct type for each partition
3. Repeat for all 3 partitions
4. Select **Write** - type `yes` to confirm
5. Select **Quit**

---

## Tips

- Replace `sdX` with your actual disk name from `fdisk -l`
- For NVMe drives it will be `/dev/nvme0n1` and partitions will be `p1`, `p2`, `p3`
- Do NOT accidentally wipe your Windows disk if dual booting - double-check the disk name!

---

[Back - Connect to Internet](./02-connect-internet.md) | [Next - Format and Mount](./04-format-mount.md)
