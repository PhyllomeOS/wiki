---
title: Phyllome OS meets a thumb drive
description: 
published: true
date: 2021-11-21T16:00:53.574Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:34:07.852Z
---

# Create an installation medium

*In this section, you will learn how to download Phyllome OS and how to create a live medium that will allow you to boot it from a thumb drive.*

> If you intent to install Phyllome OS permanently on your computer, follow this procedure but use a [Fedora Server ISO instead](https://getfedora.org/en/server/), as it is not yet possible to install Phyllome OS from the live image.
{.is-warning}

## 1. Download Phyllome OS 

The Phyllome OS ISOs files are made available [on GitHub](https://github.com/PhyllomeOS/phyllomeos/releases).

As of now, only the Phyllome OS Desktop II edition is available as an ISO file. The `II edition` is tuned for Intel CPUs and Intel GPUs. It is also known as `ldhi`, for *live*, *desktop*, *hypervisor*, and *intel*. 

* [**The direct link**](https://github.com/PhyllomeOS/phyllomeos/releases/download/v.0.2.0-alpha/phyllome-live_ldhi_v0.2.0-alpha_x86_64.iso) to download the ISO. It will take some time to load. 

> As of now, there is no checksum available, and the release is not signed using GPG keys. Among other things, it means that there is no guarantee about the authenticity of the file or its integrity, whatsoever. Alternatively, a safer is to deploy Phyllome OS [in a virtual machine](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os) or to deploy it directly on a host using [this method](/deploy/live)
{.is-warning}

## 2. Load Phyllome OS on a USB flash drive 

The following instructions may have to be adapted depending on the operating system that you are currently using.

* *General requirements*
    * A fast USB 3.0 flash drive of at least 2 GB

### Command-line instructions (Linux-only): flash a USB disk using the `dd` command line tool

The next command assumes that the ISO file is available in the *Downloads* folder and that the target medium is called `sdz`. You can identify the correct target device using the `lsblk` command line tool. Modify the command according to your context. 

> This command requires root privileges
{.is-info}

> **Warning:** This command will **destroy** any data on the target device
{.is-danger}

```
dd bs=4MB if=~/Downloads/phyllome-live_ldhi_v0.2.0-alpha_x86_64.iso of=/dev/sdz
```

### Manual instructions: flash a USB disk using Etcher

The instructions are designed with Etcher in mind. Other tools such as [Rufus](https://rufus.ie/en/), [Unetbootin](https://unetbootin.github.io/) or [Ventoy](https://www.ventoy.net/en/index.html) are likely to work too.  

> Etcher is an open-source, cross platform tool for flashing images to a target medium. It is developed and made available by [balena](https://www.balena.io/). 
{.is-info}

#### Install Etcher

You can download Etcher on [the official website](https://www.balena.io/etcher/).

Pick the right version depending on your platform.

Follow the normal procedure to install an application on your computer.

> An account with administrator rights will be needed.
{.is-info}

#### Use it

* Insert a blank flash drive on a free USB slot on your computer

* Open Etcher. You will be greeted by the screen bellow. Click on *Flash from file*

![capture-balenaetcher-1.png](/balena-etcher/capture-balenaetcher-1.png)

* Browse where the ISO is stored and select *Open*

![capture-balenaetcher-2.png](/balena-etcher/capture-balenaetcher-2.png)

* Etcher should have autodetected your USB flash drive. If this is not the case, press *Change* on the welcome screen and pick the desired destination on the new window.

![capture-balenaetcher-3.png](/balena-etcher/capture-balenaetcher-3.png)

* Select *Flash* when you are ready

> **Warning:** clicking *Flash* will **destroy** any data on the target device
{.is-danger}

> A prompt might appear, asking for your password or a confirmation.  
{.is-info}

![capture-balenaetcher-4.png](/balena-etcher/capture-balenaetcher-4.png)

* Wait a few minutes...

![capture-balenaetcher-5.png](/balena-etcher/capture-balenaetcher-5.png)

> Congratulations, the USB flash drive is now ready to use!
{.is-success}

![capture-balenaetcher-6.png](/balena-etcher/capture-balenaetcher-6.png)

## 3. Boot from a USB flash drive

Booting from an alternative 

### macOS



---

*When you are done, if you have followed the procedure with the Phyllome OS ISO, go to the section [Get started with the Live system](/getstarted/live). If you have followed the procedure using Fedora Server, with the intent of installing Phyllome OS permanently, please go to the [Install Phyllome OS page](https://wiki.phyllo.me/deploy/install) instead* 