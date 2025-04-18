---
title: Install Phyllome OS
description: 
published: true
date: 2025-04-18T22:44:03.271Z
tags: 
editor: markdown
dateCreated: 2021-11-14T16:19:00.348Z
---

# Install Phyllome OS

> Phyllome[^1] OS is an operating system that makes it easier to run [various operating systems](#go-further) locally using [off-the-shelf hardware](/deploy/prepare) and [virtualization](/virt/lexicon#virtualization) software.
{.is-info}

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

### Main flavors

Phyllome OS comes in many flavors. Pick your flavor based on the hardware you wish to deploy Phyllome on. 

The shortened URL points to the full description of the edition in a kickstart format.

| Edition | Shorthand | Features |  Shortened URL |
|---|---|---|---|
| **Phyllome OS Desktop Edition** | *PODE* | Default edition. Compatible with x86-64 CPU. GPU agnostic. IOMMU support for AMD CPUs | ks.phyllo.me/d |
| **Phyllome OS Desktop Edition for Intel:tm: CPUs** | *PODE-IC* | IOMMU and nested virtualization for Intel CPUs | ks.phyllo.me/di |
| **Phyllome OS Desktop Edition for Intel:tm: CPUs and GPUs** | *PODE-ICG* | IOMMU and nested virtualization on Intel CPUs & Intel GVT-g for Intel GPUs (from 5th to 9th gen *only*) | ks.phyllo.me/dii | 
| **Phyllome OS Desktop Edition for AMD:tm: CPUs** | PODE-AC | IOMMU and nested virtualization on AMD CPUs |  ks.phyllo.me/da |

> If you wish to learn more about how kickstart files are used to create Phyllome OS, please have a look at [the official git repository](https://git.phyllo.me/roots/phyllomeos).
{.is-info}

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

> GRUB is universal bootloader that ship with many Linux distributions
{.is-info}

### EFI-based firmware

* On the GRUB splash screen, navigate to the first entry using your keyboard arrow key and press <kbd>e</kbd>.

![kickstart-1](/assets/grub-kickstart/kickstart-2.png)

* On the new screen, use the arrow keys to place your cursor just after the word `quiet`.

![kickstart-2](/assets/grub-kickstart/kickstart-3.png)

> GRUB defaults to the US keyboard layout. Have a look at [this online resource](https://en.wikipedia.org/wiki/QWERTY#/media/File:KB_United_States.svg) to find the corresponding keys if you are not using a US keyboard layout
{.is-info}

> **Danger Zone**: the following instruction will trigger a process that will automatically **destroy** any data located on the internal disk present in your computer *without* asking for a confirmation*
{.is-danger}

* Leave a blank space after the word `quiet` and write exactly the following `inst.ks=https://ks.phyllo.me/dii`, then press <kbd>Ctrl</kbd> + <kbd>x</kbd> simultaneously or <kbd>F10</kbd>. This command will trigger the automated installation of Phyllome OS.

![kickstart-3.png](/assets/grub-kickstart/kickstart-4.png)

* During the installation process, you can use <kbd>Alt</kbd> + <kbd>Tab</kbd> to cycle through tabs, and look at the logs in real-time

![kickstart-4](/assets/grub-kickstart/kickstart-5.png)

* After a few minutes, the computer will power off

> Don't forget to remove the USB flash drive from your computer, so that next time your computer will boot, it will use the internal disk where Phyllome OS has been deployed
{.is-info}

---

*[**You are ready to get started**](https://wiki.phyllo.me/#get-started)*