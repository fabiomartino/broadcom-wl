# Broadcom Linux hybrid wireless driver 6.30.223.271

Set of patch for Broadcom wireless adapters

**Patched for Linux >= 4.15**

Tested on Debian Stretch with Kernel 4.15.2

```bash
$ uname -r
4.15.2
```

With a Azureware __BCM94360HMB__ 802.11abgn/11ac WLAN + BT PCI-E Mini Card

```bash
$ lspci -nn | grep 14e4
03:00.0 Network controller [0280]: Broadcom Limited BCM4360 802.11ac Wireless Network Adapter [14e4:43a0] (rev 03)
```

## Compile and install

* ### Clone/Download this repo:

```bash
$ git clone https://github.com/fabiomartino/broadcom-wl.git
$ cd broadcom-wl/
```
* ### Download and untarring the proper tarball:
Download the source code from [Broadcom Support and Downloads page][1]

[1]: https://www.broadcom.com/support/download-search/?pg=&pf=Wireless+LAN+Infrastructure

```bash
$ tar xzf hybrid-v35_64-nodebug-pcoem-6_30_223_271.tar.gz
```

* ### Patch the sources:

```bash
$ patch -p1 < linux-415.patch
```

* ### Build and Install
```bash
$ make clean
$ make
$ make install
$ modprobe -r bcma
$ echo "blacklist bcma" > /etc/modprobe.d/broadcom.conf
$ echo "wl" > /etc/modules-load.d/wl.conf
$ depmod -a
$ modprobe wl
```

## See also

* [Official README file][2] (download)
* Arch Linux packages: [broadcom-wl][3] / [broadcom-wl-dkms][4]
* Debian packages: [broadcom-sta][5] ([source repository][6])

[2]: https://docs.broadcom.com/docs-and-downloads/docs/linux_sta/README_6.30.223.271.txt
[3]: https://aur.archlinux.org/packages/broadcom-wl/
[4]: https://www.archlinux.org/packages/community/x86_64/broadcom-wl-dkms/
[5]: https://packages.debian.org/source/sid/broadcom-sta
[6]: https://gitlab.com/setecastronomy/broadcom-sta/tree/debian