---
title: Display
description: How to access a virtual machine's display
published: true
date: 2022-08-01T10:17:16.909Z
tags: 
editor: markdown
dateCreated: 2022-07-31T09:22:05.854Z
---

# Display

A virtual display can be attached to a virtual machine to allow interacting with it. It is a requirement for high-performance computing.

## Summary

## Specific displays

### VNC

* *to-be done*

### Spice

* *to-be done*

### SDL

The Simple DirectMedia Layer is a local-only low-latency display. 

> *It is currently only avalable with virtual machines created using the QEMU/KVM **User Session** mode.*
{.is-warning}

* Example of an XML configuration, with OpenGL enabled. This example requires 3D-capable graphic card, such as ``virtio-gpu``.

```
<graphics type="sdl" display=":0.0">
  <gl enable="yes"/>
</graphics>
```
The display resolution might not exceed that of your physical screen. 

Mouse capture doesn't work

### Xephyr

* *to-be done*


### WebRTC

* *to-be done*

### Looking Glass

* *to-be done*

### Virtio-wayland

* *to-be done*

### egl-headless

* *to-be done*

### Dbus

* *to-be done*

