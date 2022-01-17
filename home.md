---
title: Homepage
description: 
published: true
date: 2022-01-17T14:20:49.673Z
tags: 
editor: markdown
dateCreated: 2021-06-19T09:29:20.593Z
---

# Phyllome OS wiki

`Welcome to the Phyllome OS wiki! `

*In this wiki, you will find guides about how to install, use and hack Phyllome OS, as well as more general information about open-source virtualization and the project behind this specialized OS.*

***What is Phyllome OS?** [Phyllome OS](https://phyllo.me/) is an operating system that makes it easier to run various guest systems locally using [off-the-shelf hardware](https://wiki.phyllo.me/deploy/prepare). If you want to learn more about it, its goal and the context around it, have a look at the [white-paper](https://files.phyllo.me/s/oYwfxYpZcbppwr6).*

---

> If you would rather avoid JavaScript altogether, or wish to download the content of this wiki locally, feel free to clone [this repository](https://github.com/PhyllomeOS/wiki).
{.is-info}

> This is the **alpha version** of this wiki. There will be mistakes. Contributions are welcome using [Git](https://github.com/PhyllomeOS/wiki). Contributions will be possible through the web interface at a later date.
> {.is-warning}

### Deploy

*This section is meant to help users prepare their computers to host Phyllome OS, pick the version that will suit their needs, understand Phyllome OS' limitations, and install it.*

* **Choose**
	* [Is Phyllome OS right for you?](/deploy/rightforyou)
* **Install**
  * [Prepare your computer](/deploy/prepare)
  * [Create an installation medium](/deploy/medium)
  * [Install from a USB flash drive](/deploy/install) (*default method*)
	* ...and [**more**](https://wiki.phyllo.me/en/deploy)

### Get started

*This section is meant to introduce uses of Phyllome OS in a general way.*

* [Use it as a live system](/getstarted/live) (*to test it*)
* [Use it as an installed system](/getstarted/disk) (*for daily use*)

### Go further

#### Guest OS

*Although Phyllome OS thrives to pick good defaults that will work for many guest operating systems, further optimizations may be needed depending on the system you wish to use.* 

* [Install a Linux guest](/gofurther/install-guest) system using an ISO file
* [Unattended deployment of a RPM-based guest](/gofurther/virt-install) using a kickstart file
* [Install a Windows guest](/gofurther/install-windows-guest) system using an ISO file
* ...and [**more**](https://wiki.phyllo.me/en/gofurther)

*This section is meant to introduce the execution of particular taks on Phyllome OS. Some of these tasks will be rendered obsolete with newer Phyllome OS versions.*

#### Around Phyllome OS

* [Perform a few checks](/gofurther/checks) on Phyllome OS
* [Encrypt](/gofurther/encrypt) virtual disk images using filesystem-level encryption
* [Install and use the Cloud Hypervisor](/gofurther/cloud-hypervisor) to create a virtual machine
* ...and [**more**](https://wiki.phyllo.me/en/gofurther)

## On KVM virtualization

*In this section, the focus is on KVM virtualization and its associated tools, including QEMU, the Linux kernel, `libvirt`, etc., mostly in the context of Phyllome OS.*

### Hardware

* [Paravirtualized hardware](/virt/virtio) (`virtio`)
* ...and [**more**](https://wiki.phyllo.me/en/virt)

### Host

* [Linux Kernel modules](/virt/kernel-modules) related to virtualization
* ...and [**more**](https://wiki.phyllo.me/en/virt)

### Guests

* [Guests support matrix](/virt/guests)
* ...and [**more**](https://wiki.phyllo.me/en/virt)

### Resources

* [Lexicon](/virt/lexicon) 
* ...and [**more**](https://wiki.phyllo.me/en/virt)

## About Phyllome OS 

*In this section, the context around Phyllome OS is explained and its internals are described* 

* [Context](/phyllomeos/context)
* [Purpose](/phyllomeos/purpose)
* [Use cases](/phyllomeos/use-cases)
* ...and [**more**](https://wiki.phyllo.me/en/phyllomeos)

### The project

* [How to contribute](/project/contribute)
* [How to join](/project/join)
* [Current infrastructure](/project/infrastructure)

### Public presence

* **The website**: https://phyllo.me
* **This wiki**: https://wiki.phyllo.me
* **The issue board**: [https://kanboard.phyllo.me](https://kanboard.phyllo.me/b/CH7qd98J2v7egmodk/development)
* **GitHub repositories**: https://github.com/PhyllomeOS

