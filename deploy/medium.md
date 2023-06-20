---
title: Phyllome OS meets a thumb drive
description: 
published: true
date: 2021-11-23T20:30:10.268Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:34:07.852Z
---

# Create a bootable USB flash drive

*In this section, you will learn how to create a bootable USB medium that will allow you to install Phyllome on your computer.*

> As it is not yet possible to install Phyllome OS from the live image., intent to install Phyllome OS permanently on your computer, you need to use a [Fedora Server ISO instead](https://getfedora.org/en/server/). The steps below are made to be generic, and should be valid regardless of the ISO you use
{.is-info}

## Load the ISO on a USB flash drive 

The following instructions may have to be adapted depending on the operating system that you are currently using.

* *General requirements*
    * A fast USB 3.0 flash drive of at least 10 GB

### Command-line instructions (Linux-only)

This method uses the `dd` command line tool.

The next command, which requires root privileges, assumes that the ISO file is available in the *Downloads* folder and that the target medium is called `sdz`. You can identify the correct target device using the `lsblk` command line tool. Modify the command according to your context. 

> **Warning:** This command will **destroy** any data on the target device
{.is-danger}

```
dd bs=4MB if=~/Downloads/Fedora-Server-dvd-x86_64-38-1.6 of=/dev/sdz
```

### Manual instructions (Cross-platform)

The instructions are designed with Etcher in mind. Other tools such as [Rufus](https://rufus.ie/en/), [Unetbootin](https://unetbootin.github.io/) or [Ventoy](https://www.ventoy.net/en/index.html) are likely to work too.  

> Etcher is an open-source, cross platform tool for flashing images to a target medium. It is developed and made available by [balena](https://www.balena.io/)
{.is-info}

#### Install Etcher

You can download Etcher on [the official website](https://www.balena.io/etcher/).

Pick the right version depending on your platform.

Follow the normal procedure to install an application on your computer.

> An account with administrator rights will be needed
{.is-info}

#### Use it

* Insert a blank flash drive on a free USB slot on your computer

* Open Etcher. You will be greeted by the screen below. Click on *Flash from file*

![capture-balenaetcher-1.png](/assets/balena-etcher/capture-balenaetcher-1.png)

* Browse where the ISO is stored and select *Open*

![capture-balenaetcher-2.png](/assets/balena-etcher/capture-balenaetcher-2.png)

* Etcher should have autodetected your USB flash drive. If this is not the case, press *Change* on the welcome screen and pick the desired destination on the new window.

![capture-balenaetcher-3.png](/assets/balena-etcher/capture-balenaetcher-3.png)

* Select *Flash* when you are ready.

> **Warning:** clicking *Flash* will **destroy** any data on the target device
{.is-danger}

> A prompt might appear, asking for your password or a confirmation
{.is-info}

![capture-balenaetcher-4.png](/assets/balena-etcher/capture-balenaetcher-4.png)

* Wait for a few minutes...

![capture-balenaetcher-5.png](/assets/balena-etcher/capture-balenaetcher-5.png)

> Congratulations, the USB flash drive is now ready to use!
{.is-success}

![capture-balenaetcher-6.png](/assets/balena-etcher/capture-balenaetcher-6.png)

---

*Now that your USB flash drive is ready, please go to the [Install Phyllome OS page](https://wiki.phyllo.me/deploy/install).*