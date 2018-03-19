A slightly modified version of the officical archiso tool, including xorg and configs to create a dual-boot USB with Windows installation media

# Building

Same as always (https://wiki.archlinux.org/index.php/Archiso), `pacman.conf` needs some tweaking to point to a repository that has all the required AUR packages built (see `packages.both`).

# Partitions

Device: `/dev/sdx`

- archiso (vfat) - `/mnt/arch`
- windows (vfat/ntfs) - `/mnt/win`
- cowspace (ext4, label `ARCHISO_COW`)

# Installing

1. Write contents of ISO to `/mnt/arch`

2. `woeusb win.iso /dev/sdx[n]` (= `/mnt/win`)

3. `mv /mnt/win/efi/boot/{bootx64,windows}.efi`

4. Install grub:
   `grub-install --target=x86_64-efi --efi-directory=/mnt/arch --boot-directory=/mnt/arch --removable --recheck`
   `grub-install --target=i386-pc --boot-directory=/mnt/arch --recheck /dev/sdx`

5. Copy grub config
   `cp archiso/grub.cfg /mnt/arch/grub/`

6. Change values in grub config:
   * `archiso_uuid` and `windows_uuid` to the filesystem UUID of `/mnt/arch` and `/mnt/win` (i.e. from `lsblk -f`)
   * `archiso_basedir` to the one supplied to `./build.sh -D` (default "arch")
   * `archiso_label` to the label of `/mnt/arch` (default `ARCH_%Y%m`)
