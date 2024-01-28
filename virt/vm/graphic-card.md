---
title: Move pixels around
description: 
published: true
date: 2021-11-13T17:52:22.554Z
tags: 
editor: markdown
dateCreated: 2021-11-13T17:52:22.554Z
---

# Graphic cards

Phyllome leverages 3D acceleration within guest operating systems extensively, in three different modes depending on the context.

* **vfio-pci** : Passing through a physical Graphical Processing Unit (GPU) to the guest via the `vfio-pci` driver
* **vfio-mdev** : Create multiple vGPUs that can then be passed through to multiple guests. It does require a compatible GPU
* **virtio-gpu** : Expose capabilities of the host GPU to the guest via the `virtio-gpu` driver. Compatible with most GPUs but not many guests

| Description | vfio-pci | vfio-mdev | vfio-gpu |
|---|---|---|---|
| *Performance* | Near-native performance and full features set | Near-native performance and full features set | Degraded performance and limited features set |
| *Guests support* | UNIX and non-UNIX guests | UNIX and non-UNIX guests | Works only on selected UNIX guests |
| *Driver* | No specialized driver in the guest | No specialized driver in the guest | A special driver in the guest is required |
| *Number of host GPUs* | Two GPUs in most situations | A single GPU | A single GPU |
| *GPU support* | Mostly GPU agnostic | Recent Intel integrated GPUs and some professional-grade Nvidia GPUs. Some consumer GPUs can be unlocked | Mostly GPU agnostic |

---

*[**Go to parent page**](https://wiki.phyllo.me/)*