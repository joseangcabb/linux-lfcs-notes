# Storage management

In Linux, the `lsblk -al` command is used to list all block devices, providing a detailed overview of the system's storage. Here's how it works:
- `NAME`: The device name.
- `MAJ:MIN`: The major and minor device number. This is a unique identifier for the device in the system.
- `RM`: This indicates whether the device is removable (1) or not (0).
- `SIZE`: The size of the device. This is the total storage capacity of the device.
- `RO`: This indicates whether the device is read-only. A value of 1 means it's read-only, and 0 means it's read-write.
- `TYPE`: This indicates the type of the device. It could be a disk, part (partition), lvm (Logical Volume Manager), etc.
- `MOUNTPOINT`: This is the mount point of the device if applicable. It's the directory in the system's file hierarchy where the storage of the device is made accessible.

```sh
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
partprobe  # Informs the operating system kernel about changes to the partition table. This is usually used if the disk is already mounted.

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

## Verify that a device is mounted
``` sh
mount
mount | grep '/mnt'

findmnt  # Display using a tree view.
```

## Unmount
``` sh
umount /mnt/boot/efi
umount -R /mnt

# Error unmounting when device is busy
# The `lsof` command in Linux stands for "List Open Files". It's used to identify which processes are using a file, directory, or device.
lsof /mnt
```
