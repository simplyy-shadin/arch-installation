# Step 4 - Format and Mount Partitions

> After partitioning, we format each partition with the appropriate filesystem and mount them.

---

## Format Partitions

```bash
# Format EFI partition as FAT32
mkfs.fat -F 32 /dev/sdX1

# Set up swap partition
mkswap /dev/sdX2

# Format root partition as Btrfs
mkfs.btrfs /dev/sdX3
```

> Replace `sdX1`, `sdX2`, `sdX3` with your actual partition names.

---

## Mount Partitions

```bash
# Mount root partition first
mount /dev/sdX3 /mnt

# Create boot directory and mount EFI partition
mkdir /mnt/boot
mount /dev/sdX1 /mnt/boot

# Enable swap
swapon /dev/sdX2
```

---

## Verify Mount Points

```bash
lsblk
```

You should see something like:
```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sdX      8:0    0  500G  0 disk
|-sdX1   8:1    0  512M  0 part /boot
|-sdX2   8:2    0    8G  0 part [SWAP]
`-sdX3   8:3    0  492G  0 part /mnt
```

---

## Tips

- Always mount root (`/mnt`) before creating the `/mnt/boot` directory
- Btrfs is recommended for root - it supports snapshots and is modern
- If you see all three partitions mounted correctly in `lsblk`, you're good to go

---

[Back - Disk Partitioning](./03-disk-partition.md) | [Next - Base Installation](./05-base-install.md)
