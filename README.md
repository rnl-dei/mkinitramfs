# mkinitramfs

Single script to generate a minimal initramfs to boot machines with the rootfs on mdadm software raid.

**Only supports mdadm, and nothing else.**

## How to use

Just run `mkinitramfs <file>` and if run successfully the initramfs archive will be put at the file given.

## Requirements ##

The script must run as root, and the system where it is running must have `/bin/busybox` and `/sbin/mdadm` compilled statically,
which on Gentoo only needs the packages `busybox` and `mdadm` to be installed with the `static` use-flag.

It will also include the system `/etc/mdadm.conf`, altought this can be optional.

## Rescue shell

If it cannot mount the raid root array, it will drop to a rescue (busybox) shell.

If you can manually mount the array, just exit the shell and the script will try mount the root fs again. If it succeds it will continue to boot the system as usual.

Apart from the busybox utilities and mdadm, the only available help are the commands `us` and `pt` to switch between keydoard layouts.

## Why not use an existing initramfs framework

We tried the two available options on Gentoo systems.

### Genkernel

It would refuse to generate an initramfs on machines without the kernel sources installed.
And as we only compile a few kernel versions in a single machine and use them on all servers,
we don't need or want to have the sources installed on all machines.

### Dracut

It would generate fine without the kernel sources, but would not reliably drop to a rescue
shell when having problems mounting the array.

### Advantages of our system

Even if one of the frameworks above solve those issues, our script is simple enough to do one thing and do it well.

And also:
  * Have our defaults like on the keyboard layout.
  * Does not need to be given any options by the boatloader.
  * Only needs to be updated when we change the /etc/mdadm.conf.
  * We know exactly what it does and what it does not.
