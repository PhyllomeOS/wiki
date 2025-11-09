---
title: Display
description: 
published: true
date: 2025-11-08T10:28:07.779Z
tags: 
editor: markdown
dateCreated: 2022-01-25T14:50:10.751Z
---

# Virtual displays

There are mutliple displays devices available, or screens where one can access the virtual machine graphical contents.

## D-Bus display

The D-Bus display is the newest of the bunch. It exports the VM display through D-Bus and "*allow out-of-process UIs, remote protocol servers or other interactive display usages*." 

### libkms library

A project called [**libmks**](https://gitlab.gnome.org/GNOME/libmks) is offering an implementation with `libvirt` and `QEMU`.

This project is a GTK library called "libmks" (short for Mouse, Keyboard, Screen) that provides a way to interact with QEMU virtual machines through D-Bus.

It allows GTK applications to display and control VM screens, keyboards, and mice.

Key komponents:

1. **MksDisplay** - A GTK widget that displays the VM screen content, handling the visual representation and user interaction (mouse, keyboard, touch).
2. **MksScreen** - Represents a VM screen that can be connected to a display widget. It provides access to screen properties and allows configuration of screen dimensions.
3. **MksKeyboard/MksMouse/MksTouchable** - Abstractions for virtualized QEMU devices that allow sending input events (key presses, mouse clicks/moves, touch events) to the VM.
4. **MksSession** - Manages the connection to a QEMU instance via D-Bus, discovering available devices and providing access to them.
5 **MksPaintable** - A GDK paintable object that receives rendering updates from QEMU, supporting both traditional framebuffer updates and DMA-BUF based updates for better performance.

The library uses D-Bus communication with QEMU's display interface to:

- Attach to VM screens and receive visual updates
- Send keyboard/mouse/touch events to the VM
- Configure screen properties                          
- Handle clipboard sharing

It's designed to work with QEMU's D-Bus display interface and provides a GTK-friendly API for integrating VM displays into GTK applications. The library supports both synchronous and asynchronous operations for all its functions.

The project uses GTK 4, GIO, and various GTK components for the UI integration, with D-Bus for communication with QEMU.

## Resource: 

- [D-Bus display page](https://www.qemu.org/docs/master/interop/dbus-display.html#) on QEMU documentation website 