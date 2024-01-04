# Set up using Iso image

## Setup terminal for instalation
Set the keyboard layout to continue the instalation. (for me: latinamerican layout)
```
loadkeys la-latin1
```
---
Check internet connection. If ping does not respond, you will need to configure wireless connection.
```
ping google.com
````
---
Remove partition table in the disk `/dev/sda`
```
wipefs -a /dev/sda
```
---
Recreate GPT partition table
```
sgdisk -Z /dev/sda
```
---
Create partitions, use the in-console interface:

* 5550MB for EFI System [Efi System]
* 5G for Swap (Recommended size: twice the maximum memory) [Linux Swap]
* Remaining for main Filesystem [Linux Filesystem]
```
cfdisk
```
---
Format Efi Partition (`fat32`)
```
mkfs.fat -F32 /dev/sda1
```
---
Format and activate Swap Partition (`Swap`)
```
mkswap /dev/sda2
swapon /dev/sda2
```
---
Format Main File System (`ext4`)
```
mkfs.ext4 /dev/sda3
```
---
Mount Both Efi and Main Filesystem partitions
```
mount /dev/sda3 /mnt
mkdir -p /mnt/boot
mount /dev/sda1 /mnt/boot
```
---
Generate fstab file
```
genfstab -U /mnt >> /mnt/etc/fstab
```

