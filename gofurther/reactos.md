---
title: ReactOS
description: 
published: true
date: 2022-01-20T13:26:23.710Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:52:33.257Z
---

# ReactOS 

[ReactOS](https://reactos.org/) is an open-source operating system meant to behave exactly like Windows XP, Windows Server 2003 and later versions of Windows.

In theory, it can run any software and work with any drivers developed for these older versions of Windows. Decades old software or pieces of equipments that no longer ship with drivers to run with the latest iterations of the Windows operating system may work with ReactOS.

In practice, it is still under heavy-development and may not work as expected.

> **Phyllome OS support**
Support for the more modern PCI-Express-enabled Q35 chipset, UEFI or other virtio-devices, which Phyllome OS favors, is still lacking in ReactOS. Performance of the display won't be optimal, resulting in screen tearing. More information can be found [here](/virt/guest/reactos).
{.is-warning}

## Installation

> ReactOS is currently in **Alpha stage** and not production ready.  
{.is-warning}

There are basically three steps you need to make before you can use this binary-compatible and open-source replica of Windows: 

* Download a medium to install the system
* Install the system
* Configure the system

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

![reactos_installation-0.png](/wiki/assets/reactos/reactos_installation-0.png)

> The installer supports navigation using the keyboard only.
{.is-info}

* *Choose the language for the installation process, using the keyboard Arrows Keys*

![reactos_installation-1.png](/wiki/assets/reactos/reactos_installation-1.png)

* *Press <kbd>ENTER</kbd>*

![reactos_installation-2.png](/wiki/assets/reactos/reactos_installation-2.png)

* *Press <kbd>ENTER</kbd> once again*

![reactos_installation-3.png](/wiki/assets/reactos/reactos_installation-3.png)

* *Navigate to "Accept these device settings" and press <kbd>ENTER</kbd>*

![reactos_installation-4.png](/wiki/assets/reactos/reactos_installation-4.png)

* *Press <kbd>ENTER</kbd> again to select the Unpartitionned space*

![reactos_installation-5.png](/wiki/assets/reactos/reactos_installation-5.png)

* *Press <kbd>ENTER</kbd> to select the FAT file-system.*

![reactos_installation-6.png](/wiki/assets/reactos/reactos_installation-6.png)

> *Amazingly, the [BTRFS](https://en.wikipedia.org/wiki/Btrfs) file system is also supported.*
{.is-info}

* *Press <kbd>ENTER</kbd> again to format the targeted partition using the selected file system.*

![reactos_installation-7.png](/wiki/assets/reactos/reactos_installation-7.png)

* *Once the formatting is done, press <kbd>ENTER</kbd> again to install ReactOS to the selected disk*

![reactos_installation-8.png](/wiki/assets/reactos/reactos_installation-8.png)

* *Wait for the setup to complete. It is fast, so there won't be enough time for a coffee.*

![reactos_installation-9.png](/wiki/assets/reactos/reactos_installation-9.png)

* *Once the setup is done, install the bootloader on the hard disk. The default choice seems fine. Press <kbd>ENTER</kbd> to reach the next step.*

![reactos_installation-10.png](/wiki/assets/reactos/reactos_installation-10.png)

* *The installation is done, wait a few seconds or press <kbd>ENTER</kbd> to force the system to reboot right away.*

![reactos_installation-11.png](/wiki/assets/reactos/reactos_installation-11.png)

### Go through the first boot and initial setup

* *Freeloader: ReactOS' bootloader in all its glory. Wait a few seconds or press <kbd>ENTER</kbd> to start ReactOS*

![reactos_boot-1.png](/wiki/assets/reactos/reactos_boot-1.png)

* *Some devices will be automatically installed. Wait a few seconds...*

![reactos_boot-2.png](/wiki/assets/reactos/reactos_boot-2.png)

> Starting now, your mouse can be used to navigate around.
{.is-info}

* *The first boot Wizard for ReactOS should eventually appear. Press <kbd>ENTER</kbd> or click on* "Next"

![reactos_boot-3.png](/wiki/assets/reactos/reactos_boot-3.png)

* *ReactOS relies on other Open Source projets to function, which it takes time to acknowledge. Press <kbd>ENTER</kbd> or click on "Next"*

![reactos_boot-4.png](/wiki/assets/reactos/reactos_boot-4.png)

* *ReactOS can behave as a server or as a workstation. If you are unsure, choose workstation. Press <kbd>ENTER</kbd> or click on "Next"*

![reactos_boot-5.png](/wiki/assets/reactos/reactos_boot-5.png)

* *The system language and local can be customized here. If you are satisfied with the default settings, press <kbd>ENTER</kbd> or click on "Next". Otherwise, please modify the settings.*

![reactos_boot-6.png](/wiki/assets/reactos/reactos_boot-6.png)

* *Pick a username and, optionaly, an organization, then press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.*

![reactos_boot-8.png](/wiki/assets/reactos/reactos_boot-8.png)

* *Choose an administrator password, and possibly a computer name, then press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.*

![reactos_boot-10.png](/wiki/assets/reactos/reactos_boot-10.png)

* *Make sure you pick the right timezone then press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.*

![reactos_boot-11.png](/wiki/assets/reactos/reactos_boot-11.png)

* *You can pick the theme of your liking. Press <kbd>ENTER</kbd> or click on "Next" to go to the next screen when you are done.*

![reactos_boot-12.png](/wiki/assets/reactos/reactos_boot-12.png)

* *Here, you should not have to configure anything for ReactOS to have LAN and Internet access, through the newly supported `virtio-net` device. Press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.*

![reactos_boot-13.png](/wiki/assets/reactos/reactos_boot-13.png)

* *If you wish to share files with other computers on your network, joining a Workgroup would be a first step. Press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.*

![reactos_boot-14.png](/wiki/assets/reactos/reactos_boot-14.png)

* *That's it. Press <kbd>ENTER</kbd> or click on "Finish" to reboot your computer.*

![reactos_boot-15.png](/wiki/assets/reactos/reactos_boot-15.png)

### Go through the first boot and initial setup

* *Take a few seconds to admire great splash screen*

![reactos_first-boot-1.png](/wiki/assets/reactos/reactos_first-boot-1.png)

* *The system will automatically open a session with the user you created (that is pretty clever, as there is no need to remember the password I already forgot :')). A few windows may open, prompting you to install some devices. Unless you know what you are doing, cancel these prompts to land on the pristine desktop.*

![reactos_first-boot-2.png](/wiki/assets/reactos/reactos_first-boot-2.png)

* *As already stated, support for the more modern PCI-Express-enabled Q35 chipset, UEFI or other virtio-devices is not yet there. You may still enjoy the ride, try to install these old software that has long been forgotten in a drawer or this decade old printer collecting dust, and that no operating system would dare to interact with anymore*

![reactos_first-boot-3.png](/wiki/assets/reactos/reactos_first-boot-3.png)

> Congratulations, you have successfully installed ReactOS!
{.is-success}

---

* *Are you ready to try out other operating systems or learn how to execute certain tasks? If so, please follow [the link](https://wiki.phyllo.me/e/en/gofurther/)*