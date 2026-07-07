+++
title = "Protecting Fedora Atomic workstation with LUKS and FIDO2"
weight = 0
updated = 2026-07-07

[taxonomies]
tags = ["linux", "luks", "yubikey", "security", "cryptography", "fedora", "atomic", "fido2"]
+++

## Protecting Fedora LUKS partition with FIDO2

Technically these instructions are a note to myself on how-to setup the protection and as I am currently using Fedora atomic spin these instructions apply there directly, but standard Fedora works also, but you need to use different commands to build your `initrd` for example.

## Install Fedora

Install Fedora as you would normally do and during setup protect your system partition with LUKS.

## Setup Yubikey

Lets assume your Yubikey is empty without FIDO2 pin setup. Use `ykman` to setup the PIN.

`ykman fido access change-pin` can be used to setup/change a pin on the FIDO2 application on the Yubikey device.

To install `ykman` use `rpm-ostree install yubikey-manager` if not yet available in your system. Note that in atomic spin reboot is required or use `rpm-ostree apply-live`.

## Enable FIDO2 on the LUKS partition

Now since we have all that we can modify the system.

Check with `lsblk` the hardware partition hosting the LUKS container and take a note of its dev path as we will need it next. I will use as the placeholder my systems path, yours might be different so do not copy & paste.

First its a good practise to backup the current LUKS partition headers and place them on a separate device like an USB stick `cd /var/run/media/username/usb-memory && sudo cryptsetup luksHeaderBackup /dev/nvme0n1p3 --header-backup-file nvme0n1p3.img`. This can be used to recover the current header if something goes wrong. It is important that you dont store this on the system you modify!

Now we can add the FIDO2 key to a next available slot on the LUKS partition: `sudo systemd-cryptenroll --fido2-device=auto --fido2-with-client-pin=yes /dev/nvme0n1p3`. Note: this still keeps your current password active in the slot 0.

# Rebuilding initrd

Finally we need to tell the kernel where and how it should use fido2 key with the luks partition during boot. To do this use your favorite text editor to modify the `/etc/crypttab` file. On the spesific line describing your luks partition add following additional entries:

`luks-xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx none discard,x-initrd.attach,fido2-device=auto,fido2-timeout=30s`

  The entries you should need to add are `fido2-device=auto` and `fido2-timeout=30s`. The former tells boot process to check fido2 devices and the latter enables the bootprocess to wait after entering PIN code you setup earlier to physically verify your precense and push the button on your Yubikey; without it the prompt will fail instantly back to PIN entry until the original password (Now fallback key) is asked for due to failed PIN entry prompt.

After configuration is place its time to actually rebuild initrd image. In a atomic spin this builds a new boot entry incorporating the change: `sudo rpm-ostree initramfs --enable`. If something in the configuration we did earlier is awry just boot the previous one; expect if you need to restore the LUKS header that will require additional steps that are beyond the scope of this documentation.
## Reboot

Next reboot your system and during the boot the LUKS password entry will ask for the PIN of your Yubikey after which you have 30 seconds to push its button. If you fail the pin check or if you dont have your Yubikey available then just add wrong pin code and you are dropped after few tries to the password prompt where the password originally set is accepted.

## Remove the original password

If you are feeling extremily adventurous you can ofcourse remove the password from slot 0 and only have the Yubikey available. But if you loose your FIDO2 device or it gets damaged somehow you cant recover your data; unless you recover the luks header backup again.

`sudo cryptsetup luksKillSlot /dev/nvme0n1p3 0`

During the deletion process you are asked for the FIDO2 keys PIN code and again verification touch on the button. Obviously the Yubikey needs to be attached to the system when you do this.
