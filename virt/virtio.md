---
title: On paravirtualized hardware
description: 
published: true
date: 2022-01-12T16:01:26.136Z
tags: 
editor: markdown
dateCreated: 2022-01-12T14:22:51.514Z
---

# Paravirtual hardware

*Paravirtual hardware are emulated hardware or devices that can be found in a virtual environment. Contrary to other emulated hardware, they don't intend to mimic a particular piece of real hardware. More details on the [lexicon](/virt/lexicon)*

In this section, the focus is oriented towards Virtual I/O Devices (VIRTIO), also known as the `virtio` family of devices:

## Graphical frame buffer

* [`virtio-gpu`](/virt/virtio/gpu): paravirtual GPU. 
	* Provides a subset of the host GPU capabilities to a guest virtual machine

## Video decoding/encoding

* [`virtio-video`](/virt/virtio/video): paravirtual video device
	* Provides encoding and decoding capabilities to a guest virtual machine

## Sound

* [`virtio-snd`](/virt/virtio/snd)

## Storage

* [`virtio-blk`](/virt/virtio/blk)
* [`virtio-scsi`](/virt/virtio/scsi)

## Network

* [`virtio-net`](/virt/virtio/net)

## Input devices

* [`virtio-kbd`](/virt/virtio/blk)
* [`virtio-`](/virt/virtio/scsi)


## Virtual I/O Devices specifications

> [OASIS Open](https://www.oasis-open.org/org/) is a non-profit hosting standards related to the IT sector. They host VIRTIO specifications and its technical comittee.
{.is-info}

* Below is a table showing support of `virtio` devices depending on the specification version

| **Paravirtual device** | Spec 1.0 | Spec 1.1 | Spec 1.2 |
| :- | :-: | :-: | :-: |
| *virtio-gpu* | No | No | **Yes** |
| *virtio-video* | No | No | **Yes** |
| *virtio-snd* | No | No | **Yes** |
| *virtio-blk* | No | No | No |
| *virtio-scsi* | No | No | No |
| *virtio-fs* | No | No | No |
| *virtio-net* | No |  No | No |
| *virtio-keyboard* | No | No | No |
| *virtio-tablet* | No | No | No |
| *virtio-wayland* | No | No | No |
| *virtio-console* | No | No | No |

## Resources

* Specifications
	* [Version 1.0](https://docs.oasis-open.org/virtio/virtio/v1.0/virtio-v1.0.html) of the specification for Virtual I/O Devices
	* [Version 1.1](https://docs.oasis-open.org/virtio/virtio/v1.1/csprd01/virtio-v1.1-csprd01.html) of the specification for Virtual I/O Devices
* OASIS Virtual I/O Device (VIRTIO) [Technical Commitee's Page](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=virtio)
