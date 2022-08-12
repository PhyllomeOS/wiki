---
title: Display
description: How to access a virtual machine's display
published: true
date: 2022-08-12T23:47:40.458Z
tags: 
editor: markdown
dateCreated: 2022-07-31T09:22:05.854Z
---

# Display

A virtual display can be attached to a virtual machine to se the content of it. It is a must-have for non-headless scenarios.

## Summary

* *to-be done. Add table here*.

## Specific displays

### VNC

* *to-be done*

### Spice

* *to-be done*

### SDL

The Simple DirectMedia Layer is a local-only low-latency display. 

> *SDL is currently only avalable with virtual machines created using the QEMU/KVM **User Session** mode*
{.is-info}

> *As of now, this method is not compatible with Wayland* {.is-info}

> *Mouse grab does not currently work in SDL*
{.is-warning}

#### SELinux configuration

By default, SELinux will block access to X Windows Server for the virtualization stack. 

* Set new rule

```
sudo setsebool -P virt_use_xserver 1
```

* Do some magic trick 

```
sudo ausearch -c 'qemu-system-x86' --raw | audit2allow -M my-qemusystemx86
k
```

* And another one

```
sudo semodule -X 300 -i my-qemusystemx86.pp
```

#### XML SDL

* Example of an XML SDL configuration, with OpenGL enabled. This example requires a 3D-capable graphic card to be attached to the guest computer, such as ``virtio-gpu`` or ``vfio-pci``.

```
<graphics type="sdl" display=":0.0">
  <gl enable="yes"/>
</graphics>
```
The display resolution of your newly created should not exceed that of your physical screen.

### Xephyr

* *to-be done*

### WebRTC

* *to-be done*

### Looking Glass

* *to-be done*

### virtio-wayland

* *to-be done*

### egl-headless

* *to-be done*

### Dbus

* *to-be done*
