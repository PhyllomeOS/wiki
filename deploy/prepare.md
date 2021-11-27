---
title: Preparation
description: 
published: true
date: 2021-11-27T14:51:34.121Z
tags: 
editor: markdown
dateCreated: 2021-11-15T15:39:49.074Z
---

# Prepare the host computer

## Meet the requirements

These instructions are valid for most computers that ship with Linux, Windows or macOS. 

Phyllome OS targets [x86-64 systems](https://en.wikipedia.org/wiki/X86-64) with hardware-assisted virtualization, with a strong preference for those providing IOMMU-based hardware-assisted virtualization (AMD Vi or Intel VT-d). 

> Sitting idle, Phyllome OS consumes approximately 1 CPU core and 1.5 GB of RAM. This requirement scales up with the number of virtual machines running on a dedicated host: the more the virtual machines running, the more ressources Phyllome OS will use
{.is-info}

> A CPU that supports hardware-assisted virtualization is not be enough, as the motherboard also requires to support this feature. Laptop motherboards seem to be lagging behind desktop motherboards when it comes to supporting this feature. As a result of this, desktop motherboards are usually better candidates for Phyllome OS  
{.is-warning}

### Minimum requirements for Phyllome OS Desktop

* A **x86-64** computer 
* **Hardware-assisted virtualization** enabled, first generation
    * For AMD-based configurations, it means that AMD V is available and enabled (*see next section below to learn how to enable this feature*)
    * For Intel-based configurations, it means that Intel VT-x is available and enabled
* **2-core** processor
* **4 GB** of RAM
* **SSD**-based storage device to store disk images and Phyllome OS

> For Intel-based configurations, you can check if your model supports **Intel VT-x** by following [this link](https://ark.intel.com/content/www/us/en/ark/search/featurefilter.html?productType=873&2_VTX=true).
{.is-info}

### Recommended requirements for Phyllome OS Desktop

* **x86-64** computer that supports the second generation of hardware-assisted virtualization features
* **Hardware-assisted virtualization** enabled, second generation
    * For AMD-based configurations, it means that AMD Vi is available and enabled
    * For Intel-based configurations, it means that Intel VT-d is available and enabled.
* **8-core** processor
* **16 GB** of RAM
* **NVME**-based storage device to store disk images and Phyllome OS
* Two graphics cards or a graphics card that supports vfio-mdev or SR-IOV

> For Intel-based configurations, you can check if your model supports **Intel VT-d** by following [this link](https://ark.intel.com/content/www/us/en/ark/search/featurefilter.html?productType=873&0_VTD=True).
{.is-info}

## Enable hardware-assisted virtualization

Unfortunately, even on supported computer platforms, hardware-assisted virtualization is rarely turned on by default. In other words, it is not enough for a computer platform to support hardware-assisted virtualization: it is very likely that it has to be explicitly enabled.

The process to activate this feature requires accessing the firmware configuration tool for your motherboard, which is part of your BIOS or UEFI. This process is described in the following section.

> *Did you know that the Open Virtual Machine Firmware (OVMF), which is based on [TianoCore](https://www.tianocore.org/), is the default firmware for EFI-based virtual machines? Its configuration utility can be accessed using the <kbd>Esc</kbd> key.*
{.is-info}

*The TianoCore splash screen*

![uefi_tianocore_first-screen.png](/uefi_tianocore_first-screen.png)

### Accessing the firmware

The process to access the main motherboard firmware configuration utility differ depending on which operating system is currently installed on your computer.   

#### Windows 8 and newer: command-line instructions

Press the <kbd>Win</kbd> and <kbd>X</kbd> keys simultaneously to make a context menu appears. Then press <kbd>Shift</kbd> and <kbd>a</kbd> to politely ask Windows to open `Powershell` using elevated privileges, and click on the `Yes` button to bypass the User Account Control pop-up. Finally, input the following command inside the command prompt and press `enter`.

```
shutdown /fw /r
``` 
#### Windows 8 and newer: a visual walk-through

* Open the start-up menu and write "start-up", then select *Change advanced start-up options*

![screenshot_win10pro_2021-11-17_223413.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_223413.png)

* Under the *Advanced start-up* section, click on *Restart now* 

![screenshot_win10pro_2021-11-17_220109.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_220109.png)

* Select *Troubleshoot*

![screenshot_win10pro_2021-11-17_224620.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_224620.png)
	
* Then select *Advanced options*

![screenshot_win10pro_2021-11-17_225032.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_225032.png)

* Select *UEFI Firmware Settings*

![screenshot_win10pro_2021-11-17_220153.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_220153.png)

* Hit *Restart*

![screenshot_win10pro_2021-11-17_220200.png](/windows-access-firmware/screenshot_win10pro_2021-11-17_220200.png)

* Go to the section [Modify the firmware configuration](/deploy/prepare#modify-the-firmware-configuration) to learn what to do next.

#### macOS-based computers

Hardware-assisted virtualization is a hit or miss on Apple computers, as there is no way to access the firmware configuration tool on these computers. Apple users can go to the [install section](https://wiki.phyllo.me/deploy/medium) directly, create a USB stick and hope that hardware-assisted virtualization will be supported. 

#### Other computers

Make sure the targeted computer is shut down.  

During the POST phase, you need to press a certain key to access the firmware configuration tool for your motherboard, which is part of your BIOS or UEFI. 

Just after pressing the <kbd>power</kbd> button, hit the right key to access the firmware configuration tool, usually <kbd>F2</kbd> or <kbd>Del</kbd>, but it may be another keystroke on your model.

> Do not hesitate to repeatedly press the pertinent key as soon has your computer has started, to make sure it is registered
{.is-info}

### Modify the firmware configuration

Unfortunately, most firmware configuration tool do differ, and the steps here might not be identical on your current platform. In general, the sought after features are found under the *Security* tab.

For an AMD-based computer, you need to look for references to *AMD SVM*, AMD V or AMD Vi. For an Intel-based computer, you need to look for *Intel VT-x* and *Intel VT-d*. It is also possible that the feature will be referred simply to as *Virtualization*. In that case, you may not know if it actually refers to IOMMU-based hardware-assisted virtualization.

Make sure you enable these options and choose to *save and exit* the configuration tool, which will reboot your computer.

#### A visual walk-through for Intel-based NUC

Here is a visual walk-through for an Intel NUC computer.

* After you have pressed the <kbd>F2</kbd> key on boot, this screen should appear.

![efi-1.png](/inte-efi/efi-1.png)

* Go to the *Security* tab. Under the *Security Features* menu, you will find two options, *Intel Virtualization Technology* and *Intel VT for Directed I/O (VT-d)*. 

![efi-2.png](/inte-efi/efi-2.png)

* Check these boxes

![efi-4.png](/inte-efi/efi-4.png)

Then *save and exit* the configuration tool, which will reboot your computer.

> While you are there, you could also change the boot order, to make sure that your computer will boot from an attached USB thumb drive first when it will be time to try out Phyllome OS.
{.is-info}

#### Modify the boot order permanently

This section will show you how to modify the boot order permanently, so you can boot from a USB flash drive attached to your computer, a necessary step to install or use Phyllome OS as a live system. 

* Go to the *Boot* tab

![efi_boot-order-1.png](/inte-efi/efi_boot-order-1.png)

* Under the *UEFI Boot Priority* menu, you may notice that Fedora, which is installed on the internal storage device, is in the first position    

![efi_boot-order-2.png](/inte-efi/efi_boot-order-2.png)

* Move the USB Flash Drive to the first position instead, as shown in the screenshot below

![efi_boot-order-3.png](/inte-efi/efi_boot-order-3.png)

* That's it. Save changes and exist. Note that it is advisable to revert these changes after a successful installation, or to only change the bootloader temporary.



> **Failing to activate hardware-assisted virtualization** will make running virtual machines extremly **slow**, if possible at all. If, for some reasons, it cannot be activated on your computer, for example because of a lack of hardware support, you would be better off picking a Linux distribution which doesn't require it, such as [Debian](https://www.debian.org/distrib/).   
{.is-warning}

---

*If the activation is successful, you can go to the next section [to prepare an installation medium](https://wiki.phyllo.me/deploy/medium).*