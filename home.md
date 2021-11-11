---
title: Homepage
description: 
published: true
date: 2021-11-11T16:16:24.988Z
tags: 
editor: markdown
dateCreated: 2021-06-19T09:29:20.593Z
---

# Phyllome OS wiki

Welcome to the **Phyllome's OS wiki**! 

Here, you will find guides about how to install, use and hack Phyllome OS, as well as more general infos about open-source virtualization.

> If you would rather avoid JavaScript altogether, or wish to download the content of this wiki locally, we got you covered [here](https://github.com/PhyllomeOS/wiki).
{.is-info}

*[Phyllome OS](https://phyllo.me/) is an operating system that makes it easier to run [various guest systems](/phyllomeos/guests) locally using [off-the-shelf hardware](/phyllomeos/requirements).*

## Do

### Before

* [Prepare](/do/prepare)
* [Choose](/do/choose)
* [Install](/do/install)
  * [From a live medium](/do/install/live) (*default method*)
  * [From source](/do/install/source)
  * [In a virtual machine](/do/install/vm) (*to hack it*)

### During

* [As a live system](/do/use/live) (*to test it*)
* [As an installed system](/do/use/disk) (*for daily use*)

### After

* [Perform a few checks on Phyllome OS](/tasks/checks)
* [Configure the Virtual Machine Manager](/tasks/virt-manager) manually or automatically
* [Deploy Phyllome OS inside Phyllome OS](/tasks/inception) 
* [Migrate](/tasks/migrate) an existing guest virtual machine to another Phyllome OS host
* [Resize](/tasks/resize) an existing virtual disk
* [Encrypt](/tasks/encrypt) virtual disk images using filesystem-level encryption
* [Use the Cloud Hypervisor](/tasks/cloud-hypervisor) to create a virtual machine

## References

### Phyllome OS 

* [Context](/phyllomeos/context)
* [Purpose](/phyllomeos/purpose)
* [Limitations](/phyllomeos/limitations)
* [Requirements](/phyllomeos/requirements)
* [Architecture](/phyllomeos/architecture)
* [Software bill of materials](/phyllomeos/sbom) (SBOM)
* [Roadmap](/phyllomeos/roadmap)
* [Frequently Asked Questions](/phyllomeos/faq) (FAQ)

#### Guests support

By design, Phyllome OS only supports modern UEFI-based guests operating systems compatible with virtio devices. 

> It is however possible to deploy non-UEFI compatible operating systems within these guest systems, using so-called nested virtualization.
{.is-info}

* Windows NT family
	* Windows
  * ReactOS
* Unix-like operating systems
	* Linux family
  * BSD family
  * OpenSolaris and derivatives
  * Darwin and derivatives

### On virtualization

This 

* [Linux Kernel modules](/kernel_modules) related to virtualization
* [Virtualization-related paths](/linux-paths) on Linux
* [Devices](/devices)
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
