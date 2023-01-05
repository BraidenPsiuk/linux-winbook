# linux-winbook
Run mainline Debian Linux on WinBook TW700 (and probably TW801 and TW802) tablets

# UNDER CONSTRUCTION
This repo is currently being written, I am still working through a few issues and unable to share all complete instructions at this time.

# PLEASE MAKE A BACKUP FIRST
Be sure to backup your existing Windows 8 installation before attempting this install. [More info](https://support.microsoft.com/en-us/windows/create-a-usb-recovery-drive-460091d5-1e8f-cb33-2d17-8fdef77412d5)

# Foreward
These tablets all have very similar hardware, they contain Intel Baytrail CPUs and the only differences I could find were the sizes of eMMC storage and USB Type-A host port speed classification. Please remember that these devices use the Apple USB standard so you should power them using 2.1A chargers via the Micro-USB port.

# First Boot
After launching the UEFI live installer from the USB stick (you must use a USB device and not the SD slot, it is not possible to boot off the SD slot currently), press 'C' to get an ASH shell and type in the following:
```shell
# Note: Press the TAB key when you see "[TAB]"
linux (hd1,gpt2)/boot/vmlinuz-[TAB] root=/dev/mmcblk2p2 nomodeset
initrd (hd1,gpt2)/boot/initrd.img-[TAB]
boot
```
<!--
If this fails, shutdown the system and then repeat the above steps. Use:
```shell
# Need to add more steps
```
to find correct drive and partition.
-->
# GRUB Config

First, make sure all packages are up to date
```shell
sudo apt update -y && sudo apt upgrade -y
```
Install the required packages for building GRUB
```shell
sudo apt install -y build-essential git autoconf automake systemd bison autogen autotools-dev autopoint pkg-config flex
```
