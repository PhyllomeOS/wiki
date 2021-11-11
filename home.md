---
title: Homepage
description: 
published: true
date: 2021-11-11T17:12:10.734Z
tags: 
editor: markdown
dateCreated: 2021-06-19T09:29:20.593Z
---

# Phyllome OS wiki

Welcome to the **Phyllome's OS wiki**! 

Here, you will find guides about how to install, use and hack Phyllome OS, as well as more general infos about open-source virtualization and the project behind Phyllome OS.

*[Phyllome OS](https://phyllo.me/) is an operating system that makes it easier to run various guest systems locally using [off-the-shelf hardware](/do/choose/requirements).*

> If you would rather avoid JavaScript altogether, or wish to download the content of this wiki locally, we got you covered [here](https://github.com/PhyllomeOS/wiki).
{.is-info}

## Do

### Install

> Phyllome OS is still in its infancy and not ready for production use. 
{.is-warning}

* [Prepare](/prepare)
* [Choose](/do/choose)
	* [Limitations](/do/choose/limitations)
	* [Requirements](/do/choose/requirements)
* Install
  * [From a live medium](/do/install/live) (*default method*)
  * [In a virtual machine](/do/install/vm) (*to hack it*)
  * [From source](/do/install/source)

### Use

* [Use it as a live system](/do/use/live) (*to test it*)
* [Use it as an installed system](/do/use/disk) (*for daily use*)

### Master

#### Phyllome OS

* [Perform a few checks on Phyllome OS](/tasks/checks)
* [Configure the Virtual Machine Manager](/tasks/virt-manager) manually or automatically
* [Deploy Phyllome OS inside Phyllome OS](/tasks/inception) 
* [Migrate](/tasks/migrate) an existing guest virtual machine to another Phyllome OS host
* [Resize](/tasks/resize) an existing virtual disk
* [Encrypt](/tasks/encrypt) virtual disk images using filesystem-level encryption
* [Use the Cloud Hypervisor](/tasks/cloud-hypervisor) to create a virtual machine

#### Guests systems

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

Information published here is available under 
