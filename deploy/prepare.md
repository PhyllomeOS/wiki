---
title: Preparation
description: 
published: true
date: 2021-11-18T14:07:43.767Z
tags: 
editor: markdown
dateCreated: 2021-11-15T15:39:49.074Z
---

# Prepare the host computer

## 1. Meet the requirements

These instructions are valid for x86-64 computers that do ship with Linux, Windows or macOS.

Phyllome OS targets x86 systems with hardware-assisted virtualization, with a strong preference for those providing IOMMU-based hardware-assisted virtualization (AMD Vi or Intel VT-d).

Sitting idle, Phyllome OS consumes approximately 1 CPU core and 1.5 GB of RAM. 

> This requirement scales up with the number of virtual machines running on a dedicated host: the more virtual machines are running, the more ressources Phyllome OS will use.
{.is-info}

### Minimum requirements for Phyllome OS Desktop

* **x86-64** computer that supports the first generation of hardware-assisted virtualization features
    * For AMD-based configurations, it means that AMD V is available and enabled, which is the case for most CPU models.
    * For Intel-based configurations, it means that Intel VT-x is available and enabled
* **2-core** processor
* **8 GB** of RAM
* **SSD**-based storage device to store disk images and Phyllome OS
* Any graphics card (Linux or macOS guests only)

> For Intel-based configurations, you can check if your model supports Intel VT-x by looking for your model [here](https://ark.intel.com/content/www/us/en/ark/search/featurefilter.html?productType=873&2_VTX=true).
{.is-info}

A CPU that supports hardware-assisted virtualization is not be enough, as the motherboard also requires to support this feature. Laptop motherboards seem to be lacking behind desktop motherboards when it comes to supporting this feature. 
{.is-warning}

### Recommended requirements for Phyllome OS Desktop

* **x86-64** computer that supports the second generation of hardware-assisted virtualization features
    * For AMD-based configurations, it means that AMD Vi is available and enabled, which is the case for most CPU models.
    * For Intel-based configurations, it means that Intel VT-d is available and enabled.
* **8-core** processor
* **16 GB** of RAM
* **NVME**-based storage device to store disk images and Phyllome OS
* Two graphics cards or a graphics card that supports vfio-mdev or SR-IOV

> For Intel-based configurations, you can check if your model supports Intel VT-d by looking for your model [here](https://ark.intel.com/content/www/us/en/ark/search/featurefilter.html?productType=873&0_VTD=True).
{.is-info}

## 2. Enable hardware-assisted virtualization

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

Hardware-assisted virtualization is a hit or miss on Apple computers, as there is no way to access the firmware configuration tool on these computers. Apple users can go to the install section directly, create a USB stick and hope that hardware-assisted virtualization will be supported. 

* **Other computers**

Make sure the targeted computer is shut down.  

During the POST phase, you need to press a certain key to access the firmware configuration tool for your motherboard, which is part of your BIOS or UEFI. 

Just after pressing the `power-on` button, hit the right key to access the firmware configuration tool, usually <kbd>F2</kbd> or <kbd>Del</kbd>, but it may be another keystroke on your model.

> Do not hesitate to repeatedly press the pertinent key as soon has your computer has started, to make sure it is registered.
{.is-info}

### Modify the firmware configuration

> Unfortunately, most firmware configuration tool do differ, and the steps here might not be identic on your own platform.
{.is-info}

In general, the sought after features are found under the `security` tab.

For an AMD-based computer, you need to look for references to `AMD SVM`, AMD V or AMD Vi. Conversingly, for an Intel-based computer, you need to look for `Intel VT-x` and `Intel VT-d`. It is also possible that the feature will be refered simply to as `virtualization`. In that case, you may not know it refers to IOMMU-based hardware-assisted virtualization or not.

Make sure you enable these options and choose to *save and exit* the configuration tool, which will reboot your computer.

> While you are there, you could also change the boot order, to make sure that your computer will boot from an attached USB thumb drive first when it will be time to try out Phyllome OS.
{.is-info}

> Failing to activate hardware-assisted virtualization will make running virtual machines extremly slow, if possible at all. If, for some reasons, it cannot be activated on your computer, for example because of a lack of hardware support, you would be better off picking a Linux distribution which doesn't require it, such as [Debian](https://www.debian.org/distrib/).   
{.is-warning}

---

*If the activation is successful, you can go to the next section [to prepare an installation medium](https://wiki.phyllo.me/deploy/medium).*