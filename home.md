---
title: Homepage
description: 
published: true
date: 2025-04-16T19:05:35.147Z
tags: 
editor: markdown
dateCreated: 2021-06-19T09:29:20.593Z
---

# The Phyllome OS wiki

> *Phyllome[^1] OS is an operating system that makes it easier to run [various operating systems](#go-further) locally using [off-the-shelf hardware](/deploy/prepare) and [virtualization](/virt/lexicon#virtualization) technologies*
{.is-info}

In this wiki, you will find guides about [how to install](#install) and [use](#get-started) Phyllome OS, as well as information on the [underlying technologies](#references), Phyllome OS [itself](#about-phyllome-os) and the surrounding [project](#about-the-project).


> Phyllome OS is in alpha stage of development. Expect bugs and disappointment
{.is-warning}

[^1]: According to [the Wiktionary](https://en.wiktionary.org/wiki/phyllome), Phyllome refers to the "foliar part of a plant; any organ homologous with a leaf, or [any organ] produced by metamorphosis of a leaf"

## Install

*How to install Phyllome OS*

- [Prepare the target computer](/deploy/prepare)
- [Create an installation medium](/deploy/medium)
- [Install](/deploy/install)

## Get started

*How to deploy your favorite operating systems inside Phyllome OS*

### Unix-like
	
- [Install a Linux distribution through the network](/getstarted/install-guest) 
- [Automatically provision a Linux distribution](/getstarted/virt-install)

### Windows NT

- [Install ReactOS manually](/getstarted/reactos)

## Go further

*Go further with Phyllome OS*

- [Resize](/gofurther/resize) a virtual disk
- [Encrypt](/gofurther/encrypt) a directory
- [Leverage display options](/virt/vm/display)

### Sharing ressources with a guest system

- [Share a directory](/gofurther/virtiofs)
- [Share an input device](/gofurther/evdev)
- [Share a virtual GPU](/gofurther/vfio-mdev)
- [Share a physical device](/gofurther/vfio-pci)

## Technical references

*Information about related technologies*

- [Lexicon](/virt/lexicon)
- [External resources](/virt/resources)

### Virtualization software

- [KVM-driven virtual machine monitors](/virt/host/vmms)
- [Linux Kernel modules](/virt/host/modules) related to virtualization
- [Virtualization-related paths](/virt/host/paths) on Phyllome OS
- [A libvirt XML file](/virt/host/xml)

### Virtual machine hardware

- [Chipsets](/virt/vm/chipset)
- [Firmware](/virt/vm/firmware)
- [Graphic cards](/virt/vm/graphic-card)
- [Virtual I/O (virtio) devices](/virt/vm/virtio)

## About Phyllome OS

- [A very short history](/virt/history) of virtualization
- [Context](/phyllomeos/context)
- [Purpose](/phyllomeos/purpose)
- [Roadmap](/phyllomeos/roadmap)
- [Guest operating systems support](/virt/guest.md)
- [Software bill of materials](/phyllomeos/sbom)
- [Security](/phyllomeos/security)
- [FAQ](/phyllomeos/faq)

### About the project

- [How to contribute](/project/contribute)
- [How to join](/project/join)
- [Current infrastructure](/project/infrastructure)

---

**The website**: https://phyllo.me

**This wiki**: https://wiki.phyllo.me

**The issue board**: [https://kanboard.phyllo.me](https://kanboard.phyllo.me/b/CH7qd98J2v7egmodk/development)

**The forge**: https://git.phyllo.me