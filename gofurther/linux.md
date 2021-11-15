---
title: Linux
description: 
published: true
date: 2021-11-14T18:41:11.183Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:50:48.789Z
---

## Go further

*This section is meant to introduce how to execute particular taks on Phyllome OS, including deployment of certain guest systems. Some of these tasks will be rendered obsolete with newer Phyllome OS versions.*

### Tasks related to Phyllome OS

* [Perform a few checks](/gofurther/checks) on Phyllome OS
* [Configure the Virtual Machine Manager](/gofurther/virt-manager) manually or automatically
* [Install a guest system using netboot.xyz](/gofurther/install-guest)
* [Use virt-install to install a guest system](/gofurther/virt-install) 
* [Deploy Phyllome OS inside Phyllome OS](/gofurther/inception)
* [Migrate](/gofurther/migrate) an existing guest virtual machine to another Phyllome OS host
* [Resize](/gofurther/resize) an existing virtual disk
* [Encrypt](/gofurther/encrypt) virtual disk images using filesystem-level encryption
* [Use the Cloud Hypervisor](/gofurther/cloud-hypervisor) to create a virtual machine

### Tasks related to your guest OS

*Although Phyllome OS strives to choose defaults that will work for many guest systems, further optimizations may be needed.* 

> By design, Phyllome OS only supports modern UEFI-based guests operating systems compatible with virtio devices and that haven't reached their end of life.
{.is-info}

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

