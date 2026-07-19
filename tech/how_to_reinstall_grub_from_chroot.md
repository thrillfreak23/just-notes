# How to reinstall grub from a chroot

# Step 1: Open a Terminal in Debian
## Boot into Debian, open your terminal, and switch to the root user:
```code bash

sudo -s
```


# Step 2: Mount Artix and Bind System Directories
## Mount your Artix partition (sda1) to /mnt:
```code bash

mount /dev/sda1 /mnt
```


### Bind the required virtual filesystems from your running Debian system into the Artix mount point:
```code bash

for dir in dev dev/pts proc sys run; do
    mount --bind /$dir /mnt/$dir
done
```

# Step 3: Enter the Artix Chroot
## Chroot into Artix using its native shell:
```code bash

chroot /mnt /bin/bash
```


### (You are now executing commands inside your Artix system).
# Step 4: Reinstall and Update GRUB
## Install the Artix GRUB bootloader to the MBR of the drive: 
```code bash

grub-install --target=i386-pc /dev/sda
```


### Generate the new configuration file using Artix's /etc/default/grub:
```code bash

grub-mkconfig -o /boot/grub/grub.cfg
```


# Step 5: Exit and Safely Unmount
## Exit the Artix environment:
```code bash

exit
```


## Unmount all the directories safely from your Debian system:
```code bash

umount -R /mnt
```

Use code with caution.
You can now safely restart your computer. Your ThinkPad T520 will boot using the Artix GRUB configuration.
