---
title: Move pixels around
description: 
published: true
date: 2021-11-13T17:52:22.554Z
tags: 
editor: markdown
dateCreated: 2021-11-13T17:52:22.554Z
---

> Section under construction.
{.is-warning}

# Graphics cards

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
