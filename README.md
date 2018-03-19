# Partitions

- archiso (vfat) - `/mnt/usb`
- windows (vfat/ntfs) - `/mnt/win`
- cowspace (ext4, label `ARCHISO_COW`)

# Installing

Write contents of ISO to /mnt/usb

`woeusb win.iso /dev/sd[x][n]` (= `/mnt/win`)

`mv /mnt/win/efi/boot/{bootx64,windows}.efi`

`grub-install --target=x86_64-efi --efi-directory=/mnt/usb --boot-directory=/mnt/usb --removable --recheck`
`grub-install --target=i386-pc --boot-directory=/mnt/usb --recheck /dev/sd[x]`

`cp archiso/grub.cfg /mnt/usb/grub/`
