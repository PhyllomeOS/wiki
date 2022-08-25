---
title: Share an input device with a guest using evdev
description: 
published: true
date: 2022-08-25T20:26:02.610Z
tags: 
editor: markdown
dateCreated: 2022-08-13T00:26:02.801Z
---

# Share an input device

> *Input grabbing on Wayland doesn't currently work as expected. Destkop environments based on the X session manager may work better in this regard*
{.is-warning}

There are multiple ways to share an input device with a virtual machine. 

## Event device

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
sudo cat /dev/input/by-path/pci-0000:09:00.0-event-mouse
```

```
��c      $
��c���c���c�$��c�$��c׏��c׏��c
��c                          3
��c����c����cd���cd���c�2��c�2��cz��cz��c�Q��c�Q��c����c����c����c����cda
                                                                         ��cda
```    
