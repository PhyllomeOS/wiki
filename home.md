---
title: Homepage
description: 
published: true
date: 2023-05-20T21:39:28.769Z
tags: 
editor: markdown
dateCreated: 2021-06-19T09:29:20.593Z
---

# The Phyllome OS wiki

*Phyllome[^1] OS is an operating system that makes it easier to run [various operating systems](#go-further) locally using [off-the-shelf hardware](/deploy/prepare) and [virtualization](/virt/lexicon#virtualization) technologies.*

In this wiki, you will find guides about [how to install](#install) and [use](#get-started) Phyllome OS, as well as information on the [underlying technologies](#references), Phyllome OS [itself](#about-phyllome-os) and the surrounding [project](#about-the-project).

[^1]: According to [the Wiktionary](https://en.wiktionary.org/wiki/phyllome), Phyllome refers to the "foliar part of a plant; any organ homologous with a leaf, or [any organ] produced by metamorphosis of a leaf"

> If you wish to download the content of this wiki locally, feel free to clone [this repository](https://github.com/PhyllomeOS/wiki).
{.is-info}

## Install

*How to install Phyllome OS*

- [Prepare your computer](/deploy/prepare)
- [Create an installation medium](/deploy/medium)
- [Install from a USB flash drive](/deploy/install)

## Get started

*How to deploy common operating systems inside Phyllome OS*

### Unix-like
	
- [Install](/getstarted/install-guest) a Linux guest system using an ISO file
- [Automatically deploy](/getstarted/virt-install) an RPM-based guest system with `virt-install` and a kickstart file

### Windows NT

- [Install ReactOS](/getstarted/reactos)

## Go further

*Go further with Phyllome OS*

- [Use Phyllome OS as a live system](/gofurther/live)
- [Resize](/gofurther/resize) an existing virtual disk
- [Encrypt](/gofurther/encrypt) a directory containing virtual disk images
- [Share a directory](/gofurther/virtiofs) with a guest using `virtiofs`
- [Share an input device](/gofurther/evdev) with a guest using `evdev`
- [Configure](/gofurther/vfio-mdev) `vfio-mdev`

## References

*Information about technologies used by Phyllome OS*

- [A very short history](/virt/history) of virtualization
- [Lexicon](/virt/lexicon)
- [External resources](/virt/resources)

### Guest operating systems

- [Running guest operating systems with KVM](/virt/guest.md)

### The host operating system

- [Linux Kernel modules](/virt/host/modules) related to virtualization
- [Virtualization-related paths](/virt/host/paths) on Phyllome OS
- [A libvirt XML](/virt/host/xml) commented
- [Virtual I/O Devices](/virt/vm/virtio) (`virtio`)

### (Virtual) hardware

- [Chipset](/virt/vm/chipset)
- [Firmware](/virt/vm/firmware)
- [Display](/virt/vm/display)
- [Input](/virt/vm/input)
- [Graphic cards](/virt/vm/graphic-card)

## About Phyllome OS

- [Context](/phyllomeos/context)
- [Purpose](/phyllomeos/purpose)
- [Roadmap](/phyllomeos/roadmap)
- [How to contribute](/project/contribute)
- [How to join](/project/join)
- [Current infrastructure](/project/infrastructure)
- [Software bill of materials](/phyllomeos/sbom)
- [Security](/phyllomeos/security)
- [FAQ](/phyllomeos/faq)

### Public presence

- **The website**: https://phyllo.me
- **This wiki**: https://wiki.phyllo.me
- **The issue board**: [https://kanboard.phyllo.me](https://kanboard.phyllo.me/b/CH7qd98J2v7egmodk/development)
- **GitHub's repositories**: https://github.com/PhyllomeOS

