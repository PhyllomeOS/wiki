---
title: Install Phyllome OS
description: 
published: true
date: 2022-11-01T19:59:08.389Z
tags: 
editor: markdown
dateCreated: 2021-11-14T16:19:00.348Z
---

# Install Phyllome OS

*This page is intended for users that would like to install Phyllome OS permanently on their computer. To use it as a live system, please [see this page](https://wiki.phyllo.me/getstarted/live).* 

Installing Phyllome OS means booting from a [bootable USB flash drive](/deploy/medium) and fetching [an online kickstart file](https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/leaves/flat-dhi.cfg). A kickstart file contains instructions to automatically deploy an operating system.

* General requirements:
	* **A bootable USB flash drive**
	   * *If you don't have a USB flash drive ready to use, please go back to [the last section](https://wiki.phyllo.me/deploy/medium)*
  * **A wired Internet connection**
  	 * *Many files will be fetched online during the installation process*  
  * **A storage device**
  	* *The kickstart file will look for a storage device and install Phyllome OS on it. If there is no disk available, the installation will fail* 

## Create a bootable USB flash drive

> *As of now, it is only possible to deploy Phyllome OS from an [**official Fedora Everything ISO file**](https://alt.fedoraproject.org/en/)*. 
{.is-info}

* Go back to [the last section](https://wiki.phyllo.me/deploy/medium) to learn how to create a bootable USB flash drive.

## Boot from the USB flash drive

The following section illustrates how to change the boot order *temporarily*. The process to change the boot order depends on your current computer platform. Please follow the instruction that matches your platform.

### macOS

* Make sure that your computer is turned-off. 
* Plug the USB flash drive loaded with the official Fedora ISO.
* Locate the <kbd>Alt</kbd> / <kbd>Option</kbd> key on your keyboard.
* Turn your computer on and immediately hold down the <kbd>Alt</kbd> / <kbd>Option</kbd> key.
* The startup manager should appear after a few seconds.
* Click on the option called *EFI* and the GRUB splash screen will appear. Go to the section below to learn what to do next.

![kickstart-1](/assets/grub-kickstart/kickstart-1.png)

## Alter the GRUB instructions

> GRUB is universal bootloader that ship with many Linux distributions. It is a software made to find and load operating systems during a boot process.
{.is-info}

One needs to alter the GRUB instructions before the USB flash drive can load the Anaconda Installer, which is normally used to install Fedora and other related distributions. If Fedora is already installed on your computer, and if your GRUB is not password protected, which is the default behavior, you may also be able to follow the instructions below.

### EFI-based firmware

* On the GRUB splash screen, navigate to the first entry using your keyboard arrow key and press <kbd>e</kbd>.

![kickstart-1](/assets/grub-kickstart/kickstart-2.png)

* On the new screen, use the arrow keys to place your cursor just after the word `quiet`.

![kickstart-2](/assets/grub-kickstart/kickstart-3.png)

> *GRUB defaults to the US keyboard layout. Have a look at [this online resource](https://en.wikipedia.org/wiki/QWERTY#/media/File:KB_United_States.svg) to find the corresponding keys if you are not using a US keyboard layout*
{.is-info}

> ***Danger Zone**: the next instruction will trigger a process that will automatically **destroy** any data located on the internal disk present in your computer*
{.is-danger}

* Leave a blank space after the word `quiet` and write exactly the following `inst.ks=https://ks.phyllo.me/dii`, then press <kbd>Ctrl</kbd> + <kbd>x</kbd> simultaneously or <kbd>F10</kbd>. This command will trigger the automated installation of Phyllome OS. 

![kickstart-3.png](/assets/grub-kickstart/kickstart-4.png)

> *The shortened URL `https://ks.phyllo.me/dii` points to the latest Desktop version of Phyllome OS, tweaked for Intel CPUs and GPUs (gen 5th to gen 9th). The shortened link points to the kickstart file available here: https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/dishes/phyllome-desktop-intelcpu-intelgpu.cfg. Any valid kickstart file may be used.*
{.is-info}

* During the installation process, you can use <kbd>Alt</kbd> + <kbd>Tab</kbd> to cycle through tabs, and look at the logs in real-time

![kickstart-4](/assets/grub-kickstart/kickstart-5.png)

* After a few minutes, you should be greeted with a welcome screen.

![kickstart-5](/assets/grub-kickstart/kickstart-6.png)

* Go to the [First-launch configuration section](/deploy/install#first-launch) to learn what to do next.

> *If you wish to learn more about how kickstart files are used to create Phyllome OS, please have a look at [the official git repository](https://github.com/PhyllomeOS/phyllomeos).*
{.is-info}

### BIOS-based firmware

> Section under construction
{.is-warning}

## First-launch

* **Welcome screen**: on first-launch, for the *Desktop edition*, you will be greeted with the GNOME Welcome Screen. As of now, only English is available out of the box. Click *Next* when you are ready.  

![first-launch-1.png](/assets/first-launch/first-launch-1.png)

* **Keyboard layout**: you can select your favorite keyboard layout by clicking on the three stacked vertical dots at the bottom of the screen.

> *By default, Phyllome OS is set to use the *fr-CH* keyboard layout. This keyboard layout is used by people living in [Romandy](https://en.wikipedia.org/wiki/Romandy), Switzerland, which is also where the original author of Phyllome OS is from.*
{.is-info}

![first-launch-2.png](/assets/first-launch/first-launch-2.png)

* **Time zone**: you can pick your current location by clicking on the map or writing it down inside the box. The time will be adjusted according to the provided location. 

![first-launch-3.png](/assets/first-launch/first-launch-3.png)

* **Online Accounts**: Phyllome OS strongly discourages the use of *Online Accounts*, and therefore provides no option here. Click on *Skip* to go to the next screen.

> *Phyllome OS is **not** designed to be a safe place for storing persistent or personal data, as it doesn't provide full-disk encryption by default. Phyllome OS instead relies on filesystem-level encryption to protect virtual machine disks, and encourage its users to rely on another layer of encryption as provided by their operating system inside their virtual machine, whenever available.*
{.is-info}

![first-launch-4.png](/assets/first-launch/first-launch-4.png)

* **Create a user account**: you are invited to create a user account, which by default will be granted administrator or root privileges. Click on *Next* when you are done.

![first-launch-5.png](/assets/first-launch/first-launch-5.png)

* **Provide a password**: please do provide a strong password. In case you ever forget it, write it down on a piece of paper and store it somewhere safe, or/and rely on an online password manager like [Bitwarden](https://bitwarden.com/) with [multi-factor authentication](https://en.wikipedia.org/wiki/Multi-factor_authentication) enabled. Click on *Next* when you are done.

> *Phyllome OS will eventually rely on the user password as provided here to decrypt the folder containing virtual machine disks. Loosing the password will mean loosing any access to the virtual machine disks.*
{.is-info}

![first-launch-6.png](/assets/first-launch/first-launch-6.png)

* **Setup complete**: Click on start *Start Using Generic*. 

![first-launch-7.png](/assets/first-launch/first-launch-7.png)

* **Provide password**: The Virtual Machine Manager is set to auto-launch, and requires elevated permission. Please provide the user password you just set up and click on *Authenticate* to start using Phyllome OS. 

![first-launch-9.png](/assets/first-launch/first-launch-9.png)

> *Congratulations, you are done!*
{.is-success}

![first-launch-10.png](/assets/first-launch/first-launch-10.png)

> *Don't forget to remove the USB flash drive from your computer, so that next time your computer will boot, it will use the internal disk where Phyllome OS has been deployed.*
{.is-info}

---

*Please go to the [Get Started section](https://wiki.phyllo.me/getstarted/disk) to learn what to do next.*










