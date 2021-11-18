---
title: Preparation
description: 
published: true
date: 2021-11-18T14:07:43.767Z
tags: 
editor: markdown
dateCreated: 2021-11-15T15:39:49.074Z
---

> Section under construction
{.is-warning}

# Prepare the host computer

## Meet the requirements

These instructions are valid for x86-64 computers that do ship with Linux, Windows or macOS.

Phyllome OS targets x86 systems with hardware-assisted virtualization, with a strong preference for those providing IOMMU as well (AMD Vi or Intel VT-d).

Sitting idle, Phyllome OS consumes approximately 1 CPU core and 1.5 GB of RAM. 

> This requirement scales up with the number of virtual machines running on a dedicated OS. 
{.is-info}

### Minimum requirements for Phyllome OS Desktop


* **x86-64** computer that supports the first generation of hardware-assisted virtualization features
    * For AMD-based configurations, it means that AMD V is available and enabled
    * For Intel-based configurations, it means that Intel VT-x is available and enabled
* **2-core** processor
* **8 GB** of RAM
* **SSD**-based storage device to store disk images and Phyllome OS
* Any graphics card (Linux or macOS guests only)

### Recommended requirements for Phyllome OS Desktop

* **x86-64** computer that supports the second generation of hardware-assisted virtualization features
    * For AMD-based configurations, it means that AMD Vi is available and enabled
    * For Intel-based configurations, it means that Intel VT-d is available and enabled
* **8-core** processor
* **16 GB** of RAM
* **NVME**-based storage device to store disk images and Phyllome OS
* Two graphics cards or a graphics card that supports vfio-mdev or SR-IOV

## Enable hardware-assisted virtualization

### Access the firmware

*The Open Virtual Machine Firmware (OVMF), which is based on the TianoCore firmware, is the default firmware for EFI-based virtual machines. It can be accessed using the <kbd>Esc</kbd> key.*

![uefi_tianocore_first-screen.png](/uefi_tianocore_first-screen.png)

* **Since Windows 8**: command-line instructions

Press the <kbd>Win</kbd> and <kbd>X</kbd> keys simultaneously to make a context menu appears. Then press <kbd>Shift</kbd> and <kbd>a</kbd> to politely ask Windows to open `Powershell` using elevated privileges, and click on the `Yes` button to bypass the User Account Control pop-up. Finally, input the following command inside the command prompt and press `enter`.

```
shutdown /fw /r
``` 
* **Since Windows 8**: a visual walk-through

* Open the start-up menu and write `start-up`, then select *Change advanced start-up options*

![screenshot_win10pro_2021-11-17_223413.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_223413.png)

* Under the *Advanced start-up* section, click on `Restart now` 

![screenshot_win10pro_2021-11-17_220109.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_220109.png)

* Select `Troubleshoot`

![screenshot_win10pro_2021-11-17_224620.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_224620.png)
	
* Then select `Advanced options`

![screenshot_win10pro_2021-11-17_225032.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_225032.png)

* Select `UEFI Firmware Settings`

![screenshot_win10pro_2021-11-17_220153.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_220153.png)

* Hit `Restart`

![screenshot_win10pro_2021-11-17_220200.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_220200.png)

* **macOS-based computers**

Hardware-assisted virtualization is a hit or miss on Apple computers, as there is no way to access the firmware on these computers. Apple users can jump to the section *Make sure that hardware-assisted virtualization is enabled* to check whether this feature is activated or not on their particular model.

* **Other computers**

Make sure the targeted computer is shut down.  

During the POST phase, you need to press a certain key to access the firmware configuration tool for your motherboard, which is part of your BIOS or UEFI. 

Just after pressing the `power-on` button, hit the right key to access the firmware configuration tool, usually <kbd>F2</kbd> or <kbd>Del</kbd>, but it depends on your model.

> Do not hesitate to repeatedly press the pertinent key to make sure it is registered.
{.is-info}

> Hardware manufacturers could not agree on a common keystroke to access the firmware configuration tool, so, if the given keys do not work out for you, please have a look at the documentation provided by the manufacturer of your computer.
{.is.info}

### Modify the firmware configuration

`to be done`

## Make sure that hardware-assisted virtualization is enabled 

`to be done`

* **Windows**

* **macOS**

* **Linux**

> Failing to activate hardware-assisted virtualization will make running virtual machines extremly slow, if possible at all. If, for some reasons, it cannot be activated on your computer, you would be better off picking a Linux distribution which doesn't require it, such as [Debian](https://www.debian.org/distrib/).   
{.is-warning}


---

*If the activation is successful, you can go to the next section [to prepare an installation medium](https://wiki.phyllo.me/deploy/medium).*