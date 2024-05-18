# Storage management

``` sh
lsblk -al  # Display all block devices.
```

## Partition schemas

### MBR (Master Boot Record)
This is an older partitioning scheme that's been around since the PC DOS era. It's still widely used today on many systems. MBR supports up to 4 primary partitions. If you want more partitions, one of these primary partitions can be turned into an extended partition, which can contain a number of logical partitions. The maximum size of an MBR partition is 2TB.

``` sh
fdisk /dev/sda
```

### GPT (GUID Partition Table)
This is a newer partitioning scheme that's part of the UEFI standard. It's meant to replace MBR. GPT supports up to 128 partitions by default and doesn't need to rely on extended and logical partitions. The maximum size of a GPT partition is much larger than MBR, with it being 9.4 ZB (Zettabytes), which is much larger than any current consumer or enterprise hard drive.

``` sh
gdisk /dev/sda

# EFI
n  # Create a new partition
1  # Partition number 1
   # Press Enter to accept the default First sector
+500M  # Last sector, size of partition - 500MB is usually enough for EFI
ef00  # Hex code for EFI System

# Root
n  # Create a new partition
2  # Partition number 2
   # Press Enter to accept the default First sector
+30G  # Last sector, size of partition - 30GB should be enough for Root
8300  # Hex code for Linux filesystem

# Swap
n  # Create a new partition
3  # Partition number 3
   # Press Enter to accept the default First sector
+8G  # Last sector, size of partition - 8GB for Swap (adjust as needed)
8200  # Hex code for Linux swap

# Home
n  # Create a new partition
4  # Partition number 4
   # Press Enter to accept the default First sector
   # Press Enter again to use all remaining space for Home
8300  # Hex code for Linux filesystem

cat /proc/partitions  # Display partitions that are currently active in the system.
partprobe  # Informs the operating system kernel about changes to the partition table.

```

## Filesystems
A filesystem is a method of storing, organizing, and accessing files and data on a storage device, such as a hard drive, SSD, or USB flash drive. It determines how data is stored and retrieved.

``` sh
# EFI
mkfs.fat -F32 /dev/sda1

# Root (Linux filesystem)
mkfs.ext4 /dev/sda2

# Swap
mkswap /dev/sda3
swapon /dev/sda3

# Home (Linux filesystem)
mkfs.ext4 /dev/sda4
```

## Mount
It is a process that makes a certain filesystem accessible to the operating system.

``` sh
# Root
mount /dev/sda2 /mnt

# EFI
mkdir -p /mnt/boot/efi
mount /dev/sda1 /mnt/boot/efi

# Home
mkdir -p /mnt/home
mount /dev/sda4 /mnt/home
```

``` sh
# Verify that a device is mounted
mount
mount | grep '^/dev'
findmnt
```
