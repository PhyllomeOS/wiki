---
title: Phyllome OS meets a thumb drive
description: 
published: true
date: 2025-04-17T21:01:10.694Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:34:07.852Z
---

# Create a bootable USB flash drive

*In this section, you will learn how to create a bootable USB flash drive that will allow you to deploy Phyllome on a target computer.*

## Requirements

- A fast USB 3.0 flash drive of at least 10 GB
- A local copy of the [Fedora Everything](https://fedoraproject.org/everything/download/) ISO file

### Command-line instructions for Unix systems

- Plug the USB 3.0 flash drive in your computer.

- Then adapt that command, which assumes that the Fedora Everything ISO file is available in the current folder and that the target device is called `sdz`. Use `lsblk` to identify it.

> This command will **destroy** any data on the target device `sdz`
{.is-danger}

```
# dd bs=4MB if=./Fedora-Everything-netinst-x86_64-41-1.4 of=/dev/sdz
```

### Manual instructions (Cross-platform)

The instructions are designed with [Etcher](https://etcher.balena.io/) in mind. Other tools such as [Rufus](https://rufus.ie/en/), [Unetbootin](https://unetbootin.github.io/) or [Ventoy](https://www.ventoy.net/en/index.html) are likely to work too.  

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

* Browse where the Fedora Everything ISO is stored and select *Open*

![capture-balenaetcher-2.png](/assets/balena-etcher/capture-balenaetcher-2.png)

* Etcher should have autodetected your USB flash drive. If this is not the case, press *Change* on the welcome screen and pick the desired destination on the new window.

![capture-balenaetcher-3.png](/assets/balena-etcher/capture-balenaetcher-3.png)

* Select *Flash* when you are ready.

> Clicking *Flash* will **destroy** any data on the target device
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