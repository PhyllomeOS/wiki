---
title: Homepage
description: 
published: true
date: 2021-11-13T10:00:55.996Z
tags: 
editor: markdown
dateCreated: 2021-06-19T09:29:20.593Z
---

# Phyllome OS wiki

`Welcome to the Phyllome's OS wiki! `

*In this wiki, you will find guides about how to install, use and hack Phyllome OS, as well as more general information about open-source virtualization and the project behind this specialized OS.*

> If you would rather avoid JavaScript altogether, or wish to download the content of this wiki locally, feel free to clone [this repository](https://github.com/PhyllomeOS/wiki).
{.is-info}

> Phyllome OS is still in its infancy and not yet ready for production use.
{.is-warning}

*[Phyllome OS](https://phyllo.me/) is an operating system that makes it easier to run various guest systems locally using [off-the-shelf hardware](https://wiki.phyllo.me/deploy/requirements).*

## Deploy

*The section is meant to help users prepare their computer to host Phyllome OS, to pick the right version that will suit their needs, to understand its limitations, and to install it.*

* **Choose**
	* [Is Phyllome OS right for you?](/deploy/rightforyou)
  * [Requirements](/deploy/requirements)
* **Install**
  * [Prepare](/deploy/prepare)
  * [Create an installation medium](/deploy/medium)
  * [Install from a live medium](/deploy/live) (*default method*)
  * [Deploy in a virtual machine](/deploy/vm) (*to hack it*)
  * [From source](/deploy/source)

## Get started

*The section is meant to introduce how to use Phyllome OS in a general way.*

* [Use it as a live system](/getstarted/live) (*to test it*)
* [Use it as an installed system](/getstarted/disk) (*for daily use*)

## Go further

*The section is meant to introduce how to execute particular taks on Phyllome OS, including deploying certain guest systems. Some of these tasks will be rendered obsolete with newer Phyllome OS version.*

#### Tasks related to Phyllome OS

* [Perform a few checks](/gofurther/checks) on Phyllome OS
* [Configure the Virtual Machine Manager](/gofurther/virt-manager) manually or automatically
* [Install a guest system using netboot.xyz](/gofurther/install-guest)
* [Deploy Phyllome OS inside Phyllome OS](/gofurther/inception)
* [Migrate](/gofurther/migrate) an existing guest virtual machine to another Phyllome OS host
* [Resize](/gofurther/resize) an existing virtual disk
* [Encrypt](/gofurther/encrypt) virtual disk images using filesystem-level encryption
* [Use the Cloud Hypervisor](/gofurther/cloud-hypervisor) to create a virtual machine

### Tasks related to your guest OS

*Although Phyllome OS thrives to pick good defaults that will work for many guest systems, further optimizations may be needed.* 

* Unix-like
	* [Linux family](/gofurther/linux)
  * [BSD family](/gofurther/bsd)
  * [OpenSolaris and derivatives](/gofurther/opensolaris)
  * [Darwin and derivatives](/gofurther/darwin)
* Windows NT
	* [Windows family](/gofurther/windows)
  * [ReactOS](/gofurther/reactos)
* Independant
	* [Sculpt OS](/gofurther/sculpt-os)
  * [Fuschia OS](/gofurther/fuschia-os)

> It is possible to deploy non-UEFI compatible operating systems within these guest systems, using so-called nested virtualization.
{.is-info}

> By design, Phyllome OS only supports modern UEFI-based guests operating systems compatible with virtio devices and that haven't reached their end of life.
{.is-info}

## On Phyllome OS 

* [Context](/phyllomeos/context)
* [Purpose](/phyllomeos/purpose)
* [Use cases](/phyllomeos/use-cases)
* [Architecture](/phyllomeos/architecture)
* [Software bill of materials](/phyllomeos/sbom) (SBOM)
* [Roadmap](/phyllomeos/roadmap)
* [Frequently Asked Questions](/phyllomeos/faq) (FAQ)
* [Guests support matrix](/phyllomeos/guests)

## On open-source virtualization

*In this section, the focus is on KVM virtualization, and its associated tools, including QEMU, the Linux kernel, libvirt, etc., mostly in the context of Phyllome OS.* 

* [Anatomy of a virtual machine](/virt/vm)
	* [Chipsets](/virt/chipset)
  * [Firmware](/virt/firmware)
  * [CPU](/virt/cpu)
  * [Memory](/virt/memory)
  * [Storage](/virt/storage)
  * [Display](/virt/display)
* [Linux Kernel modules](/virt/kernel-modules) related to virtualization
* [Virtualization-related paths](/virt/linux-paths) on Linux
* [XML](/virt/xml) commented 
* [Lexicon](/virt/lexicon) 
* [External resources](/virt/resources)

## The Phyllome OS Project

### Functionning

* [How to join](/project/join)
* [Current infrastructure](/project/infrastructure)

### Tooling

* **The website**: https://phyllo.me
* **The wiki**: https://wiki.phyllo.me
* **The internal git**: https://git.phyllo.me