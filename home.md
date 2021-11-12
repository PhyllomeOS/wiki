---
title: Homepage
description: 
published: true
date: 2021-11-12T15:40:05.315Z
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

*[Phyllome OS](https://phyllo.me/) is an operating system that makes it easier to run various guest systems locally using [off-the-shelf hardware](https://wiki.phyllo.me/deploy/choose/requirements).*

## Deploy

*The section is meant to help users prepare their computer to host Phyllome OS, to pick the right version that will suit their needs, to understand its limitations, and to install it.*

* [Choose](/deploy/choose)
	* [Is Phyllome OS right for you?](/deploy/choose/phyllomeos)
  * [Requirements](/deploy/choose/requirements)
* [Install](/deploy/install)
  * [Prepare](/deploy/install/prepare)
  * [Create an installation medium](/deploy/install/medium)
  * [From a live medium](/deploy/install/live) (*default method*)
  * [In a virtual machine](/deploy/install/vm) (*to hack it*)
  * [From source](/deploy/install/source)

## Use

*The section is meant to introduce how to use Phyllome OS in a general way.*

* [Use it as a live system](/use/live) (*to test it*)
* [Use it as an installed system](/use/disk) (*for daily use*)

## Master

*The section is meant to introduce how to execute particular taks on Phyllome OS, including deploying certain guest systems.*

#### Tasks related to Phyllome OS

* [Perform a few checks](/tasks/checks) on Phyllome OS
* [Configure the Virtual Machine Manager](/tasks/virt-manager) manually or automatically
* [Deploy Phyllome OS inside Phyllome OS](/tasks/inception) 
* [Migrate](/tasks/migrate) an existing guest virtual machine to another Phyllome OS host
* [Resize](/tasks/resize) an existing virtual disk
* [Encrypt](/tasks/encrypt) virtual disk images using filesystem-level encryption
* [Use the Cloud Hypervisor](/tasks/cloud-hypervisor) to create a virtual machine

#### Deploy guests systems

* Unix-like
	* [Linux family](/guests/linux)
  * [BSD family](/guests/bsd)
  * [OpenSolaris and derivatives](/guests/opensolaris)
  * [Darwin and derivatives](/guests/darwin)
* Windows NT
	* [Windows family](/guests/windows)
  * [ReactOS](/guests/reactos)
* Independant
	* [Sculpt OS](/guests/sculpt-os)
  * [Fuschia OS](/guests/fuschia-os)

## Learn

### Phyllome OS 

* [Context](/phyllomeos/context)
* [Purpose](/phyllomeos/purpose)
* [Use cases](/phyllomeos/use-cases)
* [Architecture](/phyllomeos/architecture)
* [Software bill of materials](/phyllomeos/sbom) (SBOM)
* [Roadmap](/phyllomeos/roadmap)
* [Frequently Asked Questions](/phyllomeos/faq) (FAQ)

### Guests support matrix

By design, Phyllome OS only supports modern UEFI-based guests operating systems compatible with virtio devices and that haven't reached their end of life. 

> It is possible to deploy non-UEFI compatible operating systems within these guest systems, using so-called nested virtualization.
{.is-info}

### About open-source virtualization

In this section, the focus is on KVM virtualization, and its associated tools, including QEMU, the Linux kernel, libvirt, etc. 

* [Anatomy of a virtual machine](/virtualization/vm)
	* [Chipsets](/virtualization/chipset)
  * [Firmware](/virtualization/firmware)
  * [CPU](/virtualization/cpu)
  * [Memory](/virtualization/memory)
  * [Storage](/virtualization/storage)
  * [Display](/virtualization/display)
* [Linux Kernel modules](/kernel_modules) related to virtualization
* [Virtualization-related paths](/linux-paths) on Linux
* [XML](/xml) commented 
* [Lexicon](/lexicon) 
* [External resources](/resources)

> If you would rather avoid JavaScript altogether, or wish to download the content locally, we got you covered: you can fetch the content locally [here](https://git.phyllo.me/home/wiki).
{.is-info}

## The Phyllome OS Project

*  **Core team**
   * [How to join](/join)
   * [Current infrastructure](/infrastructure)
* **The website**: https://phyllo.me
* **The wiki**: https://wiki.phyllo.me
* **The git**: https://git.phyllo.me