# Set up new Archlinux partition

Enter into mounted partition
```
arch-chroot /mnt
````
## Configure timezone
Choose the desired city, for me: Bogotá D.C
```
ln -sf /usr/share/zoneinfo/America/Bogota /etc/localtime
```
Set the time according to the timezone
```
hwclock --systohc
```

## Locales
Configure locales, for me I will use `en_US.UTF-8 UTF-8`.

Remove the `#` to select the locale from the list
```
nano /etc/locale.gen
```

Then, generate the locales using:
```
locale-gen
```
--- 

Now, set the global locale using:
```
echo "LANG=en_US.UTF-8" >> /etc/locale.conf
```

Now, set the default keymap for the terminal:
```
echo "KEYMAP=la-latin1" >> /etc/vconsole.conf
```

## Network
Set the hostname

```
echo "Archlinux" >> /etc/hostname
```

For hostname resolution:
* 127.0.0.1     localhost
* ::1           localhost
* 127.0.0.1     Archlinux.localdomain Archlinux
```
nano /etc/hosts
```
---
Install network manager:
```
pacman -S networkmanager
```
Enable network manager:
```
systemctl enable NetworkManager
```

## Grub

Install grub and efi manager
```
pacman -S grub efibootmgr
```

Install grub in drive:
```
grub-install --target=x86_64-efi --efi-directory=/boot
```
Create configuration file:
```
grub-mkconfig -o /boot/grub/grub.cfg
```

## Set root user password
Finally, set the root password
```
passwd
```

## Create user
To create your user:
```
useradd -m username
passwd username
usermod -aG wheel,video,audio,storage username
```
Add the new user to the sudo users
```
sudo nano /etc/sudoers
```