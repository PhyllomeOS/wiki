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

[ReactOS](https://reactos.org/) is an open-source operating system meant to behave like Windows XP, Windows Server 2003 and later versions of Windows.

In theory, it can run any software and work with any drivers developed for these older versions of Windows. In practice, it is still under heavy-development and may not work as expected.

## State of support

Support for the more modern PCI-Express-enabled Q35 chipset, UEFI or virtio-devices is still lacking in ReactOS. Performance of the display won't be optimal, resulting in screen tearing.
{.is-warning}

| **Hardware** | ReactOS 4.13 | ReactOS 4.14 |
| :- | :-: | :-: |
| *[Chipset](/virt/vm/chipset)* | i440fx | i440fx |
| *[Platform firmware](/virt/vm/firmware)* | SeaBIOS [^1] | SeaBIOS |
| *[virtio-gpu](/virt/vm/virtio)* | No | No |
| *[virtio-video](/virt/vm/virtio)* | No | No |
| *[virtio-snd](/virt/vm/virtio)* | No | No |
| *[virtio-blk](/virt/vm/virtio)* | No | No |
| *[virtio-scsi](/virt/vm/virtio)* | No | No |
| *[virtio-fs](/virt/vm/virtio)* | No | No |
| *[virtio-net](/virt/vm/virtio)* | No | **Yes** [^2] |
| *[virtio-keyboard](/virt/vm/virtio)* | No | No |
| *[virtio-tablet](/virt/vm/virtio)* | No | No |

> Porting new paravirtual devices to ReactOS would significantly improve the experience of running ReactOS inside Phyllome OS, and other virtualization solutions leveraging [paravirtual hardware](https://wiki.phyllo.me/e/en/virt/virtio). See [here](https://reactos.org/contributing/) on how you can contribute to ReactOS
{.is-info}

## Installation

> ReactOS itself is currently in **alpha stage** and not production-ready  
{.is-warning}

There are basically three steps you need to make before you can use this binary-compatible and open-source replica of Windows: 

* Download a medium to install the system
* Install the system
* Configure the system

### Download

* Go fetch the latest build of the *Boot CD* version of ReactOS on the official website: https://reactos.org/getbuilds/

> Alternatively, the latest stable release could be downloaded
{.is-info}

* Unzip it using p7zip (`dnf install p7zip`)

```
7za x reactos-bootcd-0.4.15-dev-3628-ga6bf77e-x86-gcc-lin-dbg.7z
``` 

* Copy the resulting ISO under `/var/lib/libvirt/isos/`

```
mv reactos-bootcd-0.4.15-dev-3628-ga6bf77e-x86-gcc-lin-dbg /var/lib/libvirt/isos/
```

### Launch the installer

* Clone the `legacy model` of virtual machine and, optionally, rename it.

* Add the ISO file you just downloaded and add a disk of at least 1GB using the Virtual Machine Manager.

> As of 2022, a full installation of ReactOS takes around 750MB of disk space
{.is-info}

* Power-on the virtual machine and connect to the console.

> Just as in the good ol' days, you need to press a key to start the installer. Notice the fact that an open firmware, [SeaBIOS](https://www.seabios.org/SeaBIOS), is able to boot an open-source NT-based kernel. A rare sight.
{.is-info}


![reactos_installation-0.png](/assets/reactos/reactos_installation-0.png)

> The installer supports navigation using the keyboard only.
{.is-info}

* Choose the language for the installation process, using the keyboard Arrows Keys.

![reactos_installation-1.png](/assets/reactos/reactos_installation-1.png)

* Press <kbd>ENTER</kbd>.

![reactos_installation-2.png](/assets/reactos/reactos_installation-2.png)

* Press <kbd>ENTER</kbd> once again.

![reactos_installation-3.png](/assets/reactos/reactos_installation-3.png)

* Navigate to "Accept these device settings" and press <kbd>ENTER</kbd>.

![reactos_installation-4.png](/assets/reactos/reactos_installation-4.png)

* Press <kbd>ENTER</kbd> again to select the Unpartitionned space.

![reactos_installation-5.png](/assets/reactos/reactos_installation-5.png)

* Press <kbd>ENTER</kbd> to select the FAT file-system.

![reactos_installation-6.png](/assets/reactos/reactos_installation-6.png)

* Press <kbd>ENTER</kbd> again to format the targeted partition using the selected file system.

![reactos_installation-7.png](/assets/reactos/reactos_installation-7.png)

* Once the formatting is done, press <kbd>ENTER</kbd> again to install ReactOS to the selected disk.

![reactos_installation-8.png](/assets/reactos/reactos_installation-8.png)

* Wait for the setup to complete. It is likely to be quick, so there won't be enough time for a coffee.

![reactos_installation-9.png](/assets/reactos/reactos_installation-9.png)

* Once the setup is done, install the bootloader on the hard disk. The default choice seems fine. Press <kbd>ENTER</kbd> to reach the next step.

![reactos_installation-10.png](/assets/reactos/reactos_installation-10.png)

* The installation is done, wait a few seconds or press <kbd>ENTER</kbd> to force the system to reboot right away.

![reactos_installation-11.png](/assets/reactos/reactos_installation-11.png)

### Go through the first boot and initial setup

* Freeloader: ReactOS' bootloader in all its glory. Wait a few seconds or press <kbd>ENTER</kbd> to start ReactOS.

![reactos_boot-1.png](/assets/reactos/reactos_boot-1.png)

* Some devices will be automatically installed. Wait for a few seconds...

![reactos_boot-2.png](/assets/reactos/reactos_boot-2.png)

> Starting now, your mouse can be used to navigate around.
{.is-info}

* The first boot wizard for ReactOS should eventually appear. Press <kbd>ENTER</kbd> or click on *Next*.

![reactos_boot-3.png](/assets/reactos/reactos_boot-3.png)

* ReactOS relies on other open-source projets to function. The license has to be accepted. Press <kbd>ENTER</kbd> or click on *Next*.

![reactos_boot-4.png](/assets/reactos/reactos_boot-4.png)

* ReactOS can behave as a server or as a workstation. If you are unsure, choose workstation. Press <kbd>ENTER</kbd> or click on *Next*.

![reactos_boot-5.png](/assets/reactos/reactos_boot-5.png)

* The system language and local can be customized here. If you are satisfied with the default settings, press <kbd>ENTER</kbd> or click on *Next*. Otherwise, please modify the settings.

![reactos_boot-6.png](/assets/reactos/reactos_boot-6.png)

* Pick a username and, optionaly, an organization, then press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.

![reactos_boot-8.png](/assets/reactos/reactos_boot-8.png)

* Choose an administrator password, and possibly a computer name, then press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.

![reactos_boot-10.png](/assets/reactos/reactos_boot-10.png)

* Make sure you pick the right timezone then press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.

![reactos_boot-11.png](/assets/reactos/reactos_boot-11.png)

* You can pick the theme of your liking. Press <kbd>ENTER</kbd> or click on "Next" to go to the next screen when you are done.

![reactos_boot-12.png](/assets/reactos/reactos_boot-12.png)

* Here, you should not have to configure anything for ReactOS to have LAN and Internet access, through the newly supported `virtio-net` device. Press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.

![reactos_boot-13.png](/assets/reactos/reactos_boot-13.png)

* If you wish to share files with other computers on your network, joining a Workgroup would be a first step. Press <kbd>ENTER</kbd> or click on "Next" to go to the next screen.

![reactos_boot-14.png](/assets/reactos/reactos_boot-14.png)

* That's it. Press <kbd>ENTER</kbd> or click on "Finish" to reboot your computer.

![reactos_boot-15.png](/assets/reactos/reactos_boot-15.png)

### Go through the first boot and initial setup

* Take a few seconds to admire splash screen.

![reactos_first-boot-1.png](/assets/reactos/reactos_first-boot-1.png)

* The system will automatically open a session with the user you created (that is pretty clever, as there is no need to remember the password I already forgot :')). A few windows may open, prompting you to install some devices. Unless you know what you are doing, cancel these prompts to land on the pristine desktop.

![reactos_first-boot-2.png](/assets/reactos/reactos_first-boot-2.png)

* As already stated, support for the more modern PCI-Express-enabled Q35 chipset, UEFI or other virtio-devices is not yet there. You may still enjoy the ride, try to install these old software that has long been forgotten in a drawer or this decade old printer collecting dust, and that no operating system would dare to interact with anymore.

![reactos_first-boot-3.png](/assets/reactos/reactos_first-boot-3.png)

> Congratulations, you have successfully installed ReactOS!
{.is-success}

## Resources

* [Official resource](https://reactos.org/wiki/QEMU) on running ReactOS with QEMU
* [Hardware support list](https://reactos.org/wiki/Supported_Hardware) for ReactOS
* [Git repository](https://github.com/hectorm/docker-qemu-reactos) providing a Docker image for the ReactOS operating system
* [Current effort](https://github.com/QubesOS/qubes-issues/issues/2809) to integrate ReactOS and QubesOS
* [GSoC 2018 project idea](https://reactos.org/wiki/Google_Summer_of_Code_2018_Ideas#Paravirtualization_Support) to port more paravirtualized devices to ReactOS

[^1]: Support for [UEFI](https://reactos.org/wiki/UEFI), and potentially OVMF, is under-way.
[^2]: See [here](https://doxygen.reactos.org/d1/dc8/virtio__types_8h.html#a5a27dcd221caab788e973f6964d84aa9) for the source code reference for `virtio-net` 

---

*[**Go to parent page**](https://wiki.phyllo.me/)*