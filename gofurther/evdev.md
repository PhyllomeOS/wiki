---
title: Share an input device with a guest using evdev
description: 
published: true
date: 2023-05-13T15:04:02.628Z
tags: 
editor: markdown
dateCreated: 2022-08-13T00:26:02.801Z
---

# Share an input device

In this section, we focus on sharing a locally attached input device with a guest virtual machine.

## Event device

*Libvirt* offers a low-latency way to share an input device device with a local virtual machine, using the linux evdev event interface.

Event device or simply `evdev` is a generic input event interface that is part of the Linux kernel.

The following is an XML snippet example for sharing a mouse and a keyboard.

```
<input type='evdev'>
      <source dev='/dev/input/by-path/platform-i8042-serio-1-event-mouse/'>
</input>
<input type='evdev'>
      <source dev='/dev/input/by-path/platform-i8042-serio-0-event-kbd' grab='all' repeat='on'/>
</input>
```

Replace the `platform-i8042-serio-1-event-mouse` value with the value under `/dev/input/by-path/*` or `/dev/input/by-id/*`

If there are multiple possible options, the input device has to have `event` in the name. 

```
# cat /dev/input/by-path/pci-0000:09:00.0-event-mouse
```

```
��c      $
��c���c���c�$��c�$��c׏��c׏��c                                             
```    

## Virtio-input

> Input grabbing on Wayland doesn't currently work as expected using Spice or VNC. Destkop environments based on the X session manager may work better.
{.is-warning}

