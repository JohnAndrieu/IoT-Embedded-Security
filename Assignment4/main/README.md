# Assignment 4

## 1. Have QEMU setup and well running

On Kali's VM we will install the following qemu packages by running these commands:

```bash
apt-get install qemu-system*
```
```bash
apt-get install qemu-utils*
```
```bash
apt-get install qemu-user
```
```bash
apt-get install qemu-user-static
```
```bash
apt-get install qemu-user-binfm
```
![check-version-qemu](img/check-version-qemu.png)

## 2. Build a VM for QEMU for N architectures

### 2a) Architecture1 = MIPS

To build a Debian MIPS image on QEMU I followed this tutorial: https://markuta.com/how-to-build-a-mips-qemu-image-on-debian/ which is more recent than the one proposed in the documentation of the task.

### 2b) Architecture2 = M68K

To set up Debian/m68k on qemu-system-m68k I followed this tutorial https://wiki.debian.org/M68k/QemuSystemM68k but in the list of the machine availables I don't have q800:

Thus, I tryed the other machines availables but I got error every time:

I also tryed to change the console parameter to follow the tutorial given in the documentation:

Still the same error. I also tryed to purge and reinstall qemu but it did not work.

