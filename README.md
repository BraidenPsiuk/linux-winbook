# linux-winbook
Run mainline Debian Linux on WinBook TW700 (and probably TW801 and TW802) tablets

# UNDER CONSTRUCTION
This repo is currently being written, I am still working through a few issues and unable to share all complete instructions at this time.



# PLEASE MAKE A BACKUP FIRST
Be sure to backup your existing Windows 8 installation before attempting this install. [More info](https://support.microsoft.com/en-us/windows/create-a-usb-recovery-drive-460091d5-1e8f-cb33-2d17-8fdef77412d5)



# Foreward
These tablets all have very similar hardware, they contain Intel Baytrail CPUs and the only differences I could find were the sizes of eMMC storage and USB Type-A host port speed classification. Please remember that these devices use the Apple USB standard so you should power them using 2.1A chargers via the Micro-USB port.



# Preperation
Download the [32-bit unofficial non-free Debian netinst image](https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/current/i386/iso-cd/firmware-11.6.0-i386-netinst.iso)
(I have not tested the [free firmware version](https://cdimage.debian.org/debian-cd/current/i386/iso-cd/debian-11.6.0-i386-netinst.iso))

Debian's website warns against using the live installer on devices with < 2GB RAM, but it seemed to work perfectly fine.



# First Boot
After launching the UEFI live installer from the USB stick (you must use a USB device and not the SD slot, it is not possible to boot off the SD slot currently), press 'C' to get an ASH GRUB shell and type in the following:
```shell
# Note: Press the TAB key when you see "[TAB]"
linux (hd1,gpt2)/boot/vmlinuz-[TAB] root=/dev/mmcblk2p2 nomodeset
initrd (hd1,gpt2)/boot/initrd.img-[TAB]
boot
```

If this fails and drops you to a shell with the error "ALERT! /dev/mmcblk2p2 does not exist.", don't worry. From this shell, run:
```shell
ls /dev/mmcblk*
```
Then look for the drive that has **three** partitions listed, and remember the drive number. For example, if you see:
- /dev/mmcblk**1**p1
- /dev/mmcblk**1**p2
- /dev/mmcblk**1**p3
This would mean /dev/mmcblk**1** is the correct drive to use, and you should power off the device and re-run all commands in the "First Boot" section above, substituting "/dev/mmcblk**1**p2" for "/dev/mmcblk**2**p2".



# GRUB Config

First, make sure all packages are up to date
```shell
sudo apt update -y && sudo apt upgrade -y
```

Install the required packages for building GRUB
```shell
sudo apt install -y build-essential git autoconf automake systemd bison autogen autotools-dev autopoint pkg-config flex
```

Building GRUB
```shell
cd /tmp/
```
```shell
git clone git://git.savannah.gnu.org/grub.git
```
```shell
cd grub/
```
```shell
./bootstrap
```
```shell
./autogen.sh
```
```shell
sudo ./configure --with-platform=efi --target=i386 --program-prefix=""
```
```shell
sudo make
```
```shell
cd grub-core/
```
```shell
sudo ../grub-install -d . --efi-directory /boot/efi/ --target=i386 # NOT TESTED
```
```shell
cd /boot/efi/EFI # NOT TESTED
```
```shell
sudo cp grub/grubia32.efi ubuntu/grubx64.efi # NOT TESTED
```












