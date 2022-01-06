---
title: ReactOS
description: 
published: true
date: 2022-01-06T19:05:14.351Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:52:33.257Z
---

# ReactOS 

[ReactOS](https://reactos.org/) is an open-source operating system meant to behave exactly like Windows XP, Windows Server 2003 and later versions of Windows.

In theory, it can run any software and work with any drivers developped for early version of Windows. In practice, it is still under heavy-development and may not work as expected.

## Installation

> ReactOS is currently in **Alpha stage** and does **not** work with most virtio-devices. Performance of the display interface will not be optimal.
{.is-warning}

### Download

* *Go fetch the latest build of the *Boot CD* version of ReactOS on the official website*: https://reactos.org/getbuilds/

> Alternatively, the latest stable release could be downloaded.
{.is-info}

* *Unzip it using p7zip* (`dnf install p7zip`).

```
7za x reactos-bootcd-0.4.15-dev-3628-ga6bf77e-x86-gcc-lin-dbg.7z
``` 

* *Copy the resulting ISO under* `/var/lib/libvirt/images/`

```
mv reactos-bootcd-0.4.15-dev-3628-ga6bf77e-x86-gcc-lin-dbg /var/lib/libvirt/images/
```

### Launch the installer

* *[Clone]() the `legacy model` of virtual machine and, optionally, [rename]() it*

* *[Add the ISO file]() you just downloaded and [add a disk]() of at least 1GB using the Virtual Machine Manager*

> As of 2022, a full installation of ReactOS takes around 750Mb.
{.is-info}

* *[Power-on the virtual machine]()*

* *[Connect to the console]()*

* *Just as in the good ol' days, you need to press a key to start the installer. Notice the fact that an open firmware, [SeaBIOS](https://www.seabios.org/SeaBIOS), is able to boot an open-source NT-based kernel. A rare sight.*

![reactos_installation-0.png](/screenshots/reactos_installation-0.png)

> The installer supports navigation using the keyboard only.
{.is-info}

* *Choose the language for the installation process, using the keyboard Arrows Keys*

![reactos_installation-1.png](/screenshots/reactos_installation-1.png)

* *Press <kbd>ENTER</kbd>*

![reactos_installation-2.png](/screenshots/reactos_installation-2.png)

* *Press <kbd>ENTER</kbd> once again*

![reactos_installation-3.png](/screenshots/reactos_installation-3.png)

* *Navigate to "Accept these device settings" and press <kbd>ENTER</kbd>*

![reactos_installation-4.png](/screenshots/reactos_installation-4.png)

* *Press <kbd>ENTER</kbd> again to select the Unpartitionned space*

![reactos_installation-5.png](/screenshots/reactos_installation-5.png)

* *Press <kbd>ENTER</kbd> to select the FAT file-system.*

![reactos_installation-6.png](/screenshots/reactos_installation-6.png)

> *Amazingly, the [BTRFS](https://en.wikipedia.org/wiki/Btrfs) file system is also supported.*
{.is-info}

* *Press <kbd>ENTER</kbd> again to format the targeted partition using the selected file system.*

![reactos_installation-7.png](/screenshots/reactos_installation-7.png)

* *Once the formatting is done, press <kbd>ENTER</kbd> again to install ReactOS to the selected disk*

![reactos_installation-8.png](/screenshots/reactos_installation-8.png)

* *Wait for the setup to complete. It is fast, so there won't be enough time for a coffee.*

![reactos_installation-9.png](/screenshots/reactos_installation-9.png)

* *Once the setup is done, install the bootloader on the hard disk. The default choice seems fine. Press <kbd>ENTER</kbd> to reach the next step.*

![reactos_installation-10.png](/screenshots/reactos_installation-10.png)

* *The installation is done, wait a few seconds or press <kbd>ENTER</kbd> to force the system to reboot right away.*

![reactos_installation-11.png](/screenshots/reactos_installation-11.png)

### Go through the first-boot and initial-setup

![reactos_boot-1.png](/screenshots/reactos_boot-1.png)

![reactos_boot-2.png](/screenshots/reactos_boot-2.png)

![reactos_boot-1.png](/screenshots/reactos_boot-1.png)

---

![reactos_boot-1.png](/screenshots/reactos_boot-1.png)

* Official resource https://reactos.org/wiki/QEMU


> It accepts donations: https://reactos.org/donate/

## State of support

| **Hardware** | ReactOS 4.14 |
| :-- | -- |
| *Chipset* | i440fx only |
| *Firmware* | BIOS only |
| *virtio-gpu* | No |
| *virtio-net* | **Yes** |
| *virtio-blk* | No |
| *virtio-scsi* | No |
| *virtio-keyboard* | No |
| *virtio-tablet* | No |
