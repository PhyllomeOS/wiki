---
title: Install Phyllome OS
description: 
published: true
date: 2025-04-17T21:52:13.627Z
tags: 
editor: markdown
dateCreated: 2021-11-14T16:19:00.348Z
---

# Install Phyllome OS

[^1]: According to [the Wiktionary](https://en.wiktionary.org/wiki/phyllome), Phyllome refers to the "foliar part of a plant; any organ homologous with a leaf, or [any organ] produced by metamorphosis of a leaf"

*This page is intended for users that would like to install Phyllome OS permanently on a computer. Make sure you understand what [Phyllome OS](/phyllomeos/purpose.md) is about before installing it*

Installing Phyllome OS involves booting from a [bootable USB flash drive](/deploy/medium) and fetching an online kickstart file, which contains instructions to automatically deploy Phyllome OS.

* General requirements:
	* **A bootable USB flash drive**
	   * *If you don't have a USB flash drive ready to use, please go back to [the last section](/deploy/medium)*
  * **A wired Internet connection**
  	 * *Many files will be fetched online during the installation process*
	 * *Wireless connections are not supported*  
  * **A storage device**
  	* *The kickstart file will look for a storage device and install Phyllome OS on it. If there is no disk available, the installation will fail* 

## Pick your flavor

Phyllome[^1] OS is an operating system that makes it easier to run [various operating systems](#go-further) locally using [off-the-shelf hardware](/deploy/prepare) and [virtualization](/virt/lexicon#virtualization) software.

### Main flavors

Phyllome OS comes in many flavors. Pick your flavor based on the hardware you wish to deploy Phyllome on.

| Edition | Shorthand | Features | Kickstart URL | Shortened URL |
|---|---|---|
| **Phyllome OS Desktop Edition** | PODE | Default edition. Compatible with x86-64 CPU and GPU agnostic. IOMMU support for AMD CPUs |
| **Phyllome OS Desktop Edition for Intel CPUs** | PODEIC | IOMMU and nested virtualization on Intel CPUs | 
| **Phyllome OS Desktop Edition for Intel CPUs and GPUs** | POSEICG | IOMMU and nested virtualization on Intel CPUs & Intel GVT-g for Intel GPUs (from 5th to 9th gen *only*) | 
| **Phyllome OS Desktop Edition for AMD:tm: CPUs** | PODEAC | IOMMU and nested virtualization on AMD CPUs |  |

### Other flavors

## Boot from the USB flash drive

The following section illustrates how to change the boot order *temporarily*. The process to change the boot order depends on your current computer platform. Please follow the instruction that match your platform.

### macOS

* Make sure that your computer is turned-off. 
* Plug the USB flash drive loaded with the official Fedora ISO.
* Locate the <kbd>Alt</kbd> / <kbd>Option</kbd> key on your keyboard.
* Turn your computer on and immediately hold down the <kbd>Alt</kbd> / <kbd>Option</kbd> key.
* The startup manager should appear after a few seconds.
* Click on the option called *EFI* and the GRUB splash screen will appear. Go to the section below to learn what to do next.

![kickstart-1](/assets/grub-kickstart/kickstart-1.png)

## Boot into the automated installation process

One needs to alter the GRUB instructions in order to trigger the automated installation. 

> GRUB is universal bootloader that ship with many Linux distributions.
{.is-info}

### EFI-based firmware

* On the GRUB splash screen, navigate to the first entry using your keyboard arrow key and press <kbd>e</kbd>.

![kickstart-1](/assets/grub-kickstart/kickstart-2.png)

* On the new screen, use the arrow keys to place your cursor just after the word `quiet`.

![kickstart-2](/assets/grub-kickstart/kickstart-3.png)

> GRUB defaults to the US keyboard layout. Have a look at [this online resource](https://en.wikipedia.org/wiki/QWERTY#/media/File:KB_United_States.svg) to find the corresponding keys if you are not using a US keyboard layout
{.is-info}

* Write-down the URL associated to the edition you picked

|  | Edition | Kickstart URL |
|---|---|---|
| *CPU and GPU agnostic* | **Phyllome OS Desktop** | [ks.phyllo.me/d](https://ks.phyllo.me/d) |
| *Intel CPU* | **Phyllome OS Desktop I** | [ks.phyllo.me/di](https://ks.phyllo.me/di) | 
| *AMD CPU* | **Phyllome OS Desktop A** | [ks.phyllo.me/da](https://ks.phyllo.me/da) |
| *Intel CPU and GPU* | **Phyllome OS Desktop II** | [ks.phyllo.me/dii](https://ks.phyllo.me/dii) |

> **Danger Zone**: the following instruction will trigger a process that will automatically **destroy** any data located on the internal disk present in your computer *without* asking for a confirmation*
{.is-danger}

* Leave a blank space after the word `quiet` and write exactly the following `inst.ks=https://ks.phyllo.me/dii`, then press <kbd>Ctrl</kbd> + <kbd>x</kbd> simultaneously or <kbd>F10</kbd>. This command will trigger the automated installation of Phyllome OS.

![kickstart-3.png](/assets/grub-kickstart/kickstart-4.png)

* During the installation process, you can use <kbd>Alt</kbd> + <kbd>Tab</kbd> to cycle through tabs, and look at the logs in real-time

![kickstart-4](/assets/grub-kickstart/kickstart-5.png)

* After a few minutes, you should be greeted with a welcome screen.

![kickstart-5](/assets/grub-kickstart/kickstart-6.png)

> If you wish to learn more about how kickstart files are used to create Phyllome OS, please have a look at [the official git repository](https://github.com/PhyllomeOS/phyllomeos).
{.is-info}

## First-launch

* **Welcome screen**: on first-launch, for the *Desktop edition*, you will be greeted with the GNOME Welcome Screen. As of now, only English is available out of the box. Click *Next* when you are ready.  

![first-launch-1.png](/assets/first-launch/first-launch-1.png)

* **Keyboard layout**: you can select your favorite keyboard layout by clicking on the three stacked vertical dots at the bottom of the screen.

> By default, Phyllome OS is set to use the *fr-CH* keyboard layout. This keyboard layout is used by people living in [Romandy](https://en.wikipedia.org/wiki/Romandy), Switzerland, which is also where the original author of Phyllome OS is from.
{.is-info}

![first-launch-2.png](/assets/first-launch/first-launch-2.png)

* **Time zone**: you can pick your current location by clicking on the map or writing it down inside the box. The time will be adjusted according to the provided location.

![first-launch-3.png](/assets/first-launch/first-launch-3.png)

* **Online Accounts**: Phyllome OS strongly discourages the use of *Online Accounts*, and therefore provides no option here. Click on *Skip* to go to the next screen.

![first-launch-4.png](/assets/first-launch/first-launch-4.png)

* **Create a user account**: you are invited to create a user account, which by default will be granted administrator or root privileges. Click on *Next* when you are done.

![first-launch-5.png](/assets/first-launch/first-launch-5.png)

* **Provide a password**: please do provide a strong password. In case you ever forget it, write it down on a piece of paper and store it somewhere safe, or/and rely on an online password manager like [Bitwarden](https://bitwarden.com/). Click on *Next* when you are done.

![first-launch-6.png](/assets/first-launch/first-launch-6.png)

* **Setup complete**: Click on start *Start Using Generic*. 

![first-launch-7.png](/assets/first-launch/first-launch-7.png)

* **Provide password**: The Virtual Machine Manager is set to auto-launch, and requires elevated permission. Please provide the user password you just set up and click on *Authenticate* to start using Phyllome OS. 

![first-launch-9.png](/assets/first-launch/first-launch-9.png)

> Congratulations, you are done!
{.is-success}

![first-launch-10.png](/assets/first-launch/first-launch-10.png)

> Don't forget to remove the USB flash drive from your computer, so that next time your computer will boot, it will use the internal disk where Phyllome OS has been deployed
{.is-info}

---

*[**You are ready to get started**](https://wiki.phyllo.me/#get-started)*