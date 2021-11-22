---
title: Install Phyllome OS
description: 
published: true
date: 2021-11-22T16:45:28.838Z
tags: 
editor: markdown
dateCreated: 2021-11-14T16:19:00.348Z
---

# How to install Phyllome OS

> As of now, it is only possible to deploy Phyllome OS using an **offical Fedora ISO file** and an online kickstart file. It you don't have a USB flash drive ready to use, please go back to the last section.
{.is-info}

*To install Phyllome OS permanently, you will need to plug the loaded USB flash drive to your targeted computer, to turn this computer on, to select the USB flash drive when it is booting up, and to modify a default GRUB command. These steps are explained below.* 

> If you already have Fedora installed on your computer, you may skip this section and go straight to the *Alter the GRUB instructions* section below.
{.is-info}

> This page is intended for users that would like to install Phyllome OS permanently on their computer. As a result, following these instructions will permanently modify the content of the target device, erasing it. Proceed with caution. 
{.is-warning}

## Boot from a USB flash drive

> By default, when a computer boots up, it will look for an operating system on the internal storage device first. If there is one, it will load this operating system and ignore any other media, such as any USB flash drive that may be plugged to the computer. To boot from a USB flash drive, one would have to either temporary or permanently alter the so-called boot order. The boot order instructs at what point and where it should look for an operating system. 
{.is-info}

The following section illustrates how to change the boot order *temporarily*. The process to change the boot order depends on your current computer platform. Please follow the instruction that matches your platform.

### macOS

* Make sure that your computer is turned-off. 
* Plug the USB flash drive loaded with the official Fedora ISO.
* Locate the <kbd>Alt</kbd> / <kbd>Option</kbd> key on your keyboard.
* Turn your computer on and immediately press the <kbd>Alt</kbd> / <kbd>Option</kbd> key continuously.
* The startup manager should appear after a few seconds.
* Click on the option called *EFI* and the GRUB splash screen will appear. Go to the section below to learn what to do next.

![screenshot_uefi_2021-11-22_154211.png](/grub-kickstart/screenshot_uefi_2021-11-22_154211.png)

### Windows 8 and later versions

> Section under construction
{.is-warning}

### Other computers

> Section under construction
{.is-warning}

## Alter the GRUB instructions

> GRUB is universal bootloader that ship with many Linux distributions. It is a software made to find and load operating systems during a boot process.
{.is-info}

One needs to alter the GRUB instructions before the USB flash drive can load the Anaconda Installer, which is normally used to install Fedora and other related distributions. If Fedora is already installed on your computer, and if your GRUB is not password protected, which is the default behavior, you may also be able to follow the instructions below.

### EFI-based firmware

* On the GRUB splash screen, navigate to the first entry using your keyboard arrow key and press <kbd>e</kbd>.

![screenshot_uefi_2021-11-22_154226.png](/grub-kickstart/screenshot_uefi_2021-11-22_154226.png)

* On the new screen, navigate after the *quiet* word.

![screenshot_uefi_2021-11-22_154238.png](/grub-kickstart/screenshot_uefi_2021-11-22_154238.png)

> GRUB defaults to the US keyboard layout. Have a look at [this online ressource](https://en.wikipedia.org/wiki/QWERTY#/media/File:KB_United_States.svg) to find the corresponding keys if you are having a hard time finding the right keystroke
{.is-info}

> **Danger Zone**: the next instruction will trigger an automated process that will **destroy** any data located on the internal disk in your computer. 
{.is-danger}

* Leave a blank space after the `quiet` word and write exactly the following `inst.ks=https://ks.phyllo.me/dii`, then press <kbd>Ctrl</kbd> + <kbd>x</kbd> simultaneously.

![screenshot_uefi_2021-11-22_155450.png](/grub-kickstart/screenshot_uefi_2021-11-22_155450.png)

* The command will trigger the automated installation of Phyllome OS. 

> The shortened URL `https://ks.phyllo.me/dii` points to the latest Desktop version of Phyllome OS, tweaked for Intel CPUs and GPUs. The kickstart file is available here: https://raw.githubusercontent.com/PhyllomeOS/phyllomeos/main/leaves/flat-dhi.cfg
{.is-info}

![screenshot_uefi_2021-11-11_130934.png](/grub-kickstart/screenshot_uefi_2021-11-11_130934.png)

After a few minutes, you should be greeted with a welcome screen.

![screenshot_uefi_2021-11-11_143000.png](/grub-kickstart/screenshot_uefi_2021-11-11_143000.png)

Go to the [First-launch configuration section](/deploy/install#first-launch) to learn what to do next.

### BIOS-based firmware

> Section under construction
{.is-warning}

## First-launch

> Section under construction
{.is-warning}

---

*Please go to the [Get Started section](https://wiki.phyllo.me/getstarted/disk) to learn what to do next.*










