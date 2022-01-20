---
title: On paravirtualized hardware
description: 
published: true
date: 2022-01-20T11:36:12.069Z
tags: 
editor: markdown
dateCreated: 2022-01-12T14:22:51.514Z
---

> *Section under construction*
{.is-warning}



# Paravirtual hardware

*Paravirtual hardware are emulated hardware or devices that can be found in a virtual environment. Contrary to other emulated hardware, they don't intend to mimic a particular piece of real hardware. More details on the [lexicon](/virt/lexicon)*

In this section, the focus is oriented towards Virtual I/O Devices (VIRTIO), also known as the `virtio` family of devices:

> This list is not meant to be exhaustive
{.is-info}


## Graphical frame buffer

* [`virtio-gpu`](/virt/virtio/gpu): 
	* Paravirtual GPU that provides a subset of the host GPU capabilities to a guest virtual machine

## Video decoding/encoding

* [`virtio-video`](/virt/virtio/video): 
	* Paravirtual video device that provides encoding and decoding capabilities to a guest virtual machine

## Sound

* [`virtio-snd`](/virt/virtio/snd)

## Storage

* [`virtio-blk`](/virt/virtio/blk)
* [`virtio-scsi`](/virt/virtio/scsi)
* [`virtio-fs`](/virt/virtio/fs)

## Network

* [`virtio-net`](/virt/virtio/net)

## Input devices

* [`virtio-kbd`](/virt/virtio/blk)
* [`virtio-tablet`](/virt/virtio/tabket)

## Miscellaneous

* [`virtio-rng`](/virt/virtio/rng)
* [`virtio-crypto`](/virt/virtio/crypto)
* [`virtio-balloon`](/virt/virtio/balloon)
* [`virtio-iommu`](/virt/virtio/iommu)
* [`virtio-console`](/virt/virtio/console)

## Virtual I/O Devices specifications

> [OASIS Open](https://www.oasis-open.org/org/) is a non-profit hosting standards related to the IT sector. They host VIRTIO specifications and its technical committee.
{.is-info}

* Below is a table showing support of `virtio` devices depending on the specification version

| **Paravirtual device** | Spec. 1.0 | Spec. 1.1 | Spec. 1.2 |
| :- | :-: | :-: | :-: |
| *`virtio-gpu`* | No | **Yes** | **Yes** |
| *`virtio-video`* | No | No | **Yes** |
| *`virtio-snd`* | No | No | **Yes** |
| *`virtio-blk`* | **Yes** | **Yes** | **Yes** |
| *`virtio-scsi`* | **Yes** | **Yes** | **Yes** |
| *`virtio-fs`* | No | No | ? |
| *`virtio-net`* | **Yes** |  **Yes** | **Yes** |
| *`virtio-keyboard`* | No | No | ? |
| *`virtio-tablet`* | No | No | ? |
| *`virtio-wayland`* | No | No | ? |
| *`virtio-console`* | **Yes** | **Yes** | **Yes** |

## Resources

* Specifications
	* [Version 1.0](https://docs.oasis-open.org/virtio/virtio/v1.0/virtio-v1.0.html) of the specification for Virtual I/O Devices
	* [Version 1.1](https://docs.oasis-open.org/virtio/virtio/v1.1/csprd01/virtio-v1.1-csprd01.html) of the specification for Virtual I/O Devices
* OASIS Virtual I/O Device (VIRTIO) [Technical Commitee's Page](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=virtio)
* `virtio` entry on [OSDev.org](https://wiki.osdev.org/Virtio)