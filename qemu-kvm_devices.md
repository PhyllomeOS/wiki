---
title: QEMU/KVM devices list
description: Description of pertinent devices
published: true
date: 2021-08-12T13:47:04.813Z
tags: 
editor: markdown
dateCreated: 2021-08-12T13:47:04.813Z
---

# Software-based hardware

## Chipsets

### q35

### virt

## Storage

scsi, sata, usb, virtio-serial, virtio-scsi

## Networking

## Graphics

virtio

Phyllome leverages 3D acceleration within guest operating systems extensively, in three different modes depending on the situation.

* **vfio-pci** : Passing through a complete physical Graphical Processing Unit (GPU) to the guest via the `vfio-pci` driver
* **vfio-mdev** : Sharing a fraction of a compatible physical GPU such as those using [single-root input/output virtualization](https://en.wikipedia.org/wiki/Single-root_input/output_virtualization) (SR-IOV), via the `vfio-mdev` driver
* **vfio-gpu** : Using some capabilities of the host GPU, via the `vfio-gpu` driver, which creates a virtual GPU as is used in Chromium OS and Spectrum OS

| Description | vfio-pci | vfio-mdev | vfio-gpu |
|---|---|---|---|
| *Performance* | Near-native performance and full features set | Near-native performance and full features set | Degraded performance and limited features set |
| *Guests support* | UNIX and non-UNIX guests | UNIX and non-UNIX guests | Works only on selected UNIX guests |
| *Driver* | No special driver in the guest | No special driver in the guest | Requires a special driver in the guest |
| *Number of host GPUs* | Two GPUs in most situations | A single GPU | A single GPU |
| *GPU support* | Mostly GPU agnostic | Recent Intel integrated GPUs and some professional grade Nvidia GPUs | Mostly GPU agnostic |

`ADD VIDEO HERE`


### Video-device

cirrus, vga, qxl, virtio, or vmvga (vmware)



Display
Spice VNC egl-headless GTK
Sound
Virtio-sound, ich6, ich9, ac97, es1370, sb16, pcspk