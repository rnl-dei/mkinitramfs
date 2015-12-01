# mkinitramfs

Single script to generate a minimal initramfs to boot machines with the rootfs on mdadm software raid.

**Only supports mdadm, and nothing else.**

## How to use

Just run `mkinitramfs` and if run successfully the initramfs archive will be put at /boot/initramfs-custom.

## Requirements ##

The script must run as root, and the system where it is running must have `/bin/busybox` and `/sbin/mdadm` compilled statically,
which on Gentoo only needs the packages `busybox` and `mdadm` to be installed with the `static` use-flag.

It will also include the system `/etc/mdadm.conf`, altought this can be optional.