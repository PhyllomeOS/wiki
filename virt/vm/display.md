---
title: Display
description: How to access a virtual machine's display
published: true
date: 2023-05-20T20:25:48.806Z
tags: 
editor: markdown
dateCreated: 2022-07-31T09:22:05.854Z
---

# Display

A virtual display can be attached to a virtual machine, letting a user see the content of it. It is a must-have for non-headless scenario.


## Summary

> *[Official ressource](https://libvirt.org/formatdomain.html#graphical-framebuffers) for `libvirt`-compatible displays, including various XML examples*
> 
{.is-info}

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

* The display resolution of your guest display should not exceed that of your physical screen.

#### SELinux configuration

By default, SELinux will block access to X Windows Server for the virtualization stack. An exception has to be set.

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

#### XML SDL example

* Example of an XML SDL configuration, with OpenGL enabled. This example requires a 3D-capable graphic card to be attached to the guest computer, such as ``virtio-gpu`` or ``vfio-pci``.

```
<graphics type="sdl" display=":0" fullscreen="yes">
  <gl enable="yes"/>
</graphics>
```

> *You can identify your display using the following command: `echo $DISPLAY`*
{.is-info}

### D-Bus

> *The D-Bus display is only available since version 7.4.0 of *`libvirt`**
{.is-warning}

[D-Bus](https://www.freedesktop.org/wiki/Software/dbus/) is a  Desktop-oriented middleware that can be used to create a display for a virtual machine.  

> *[Detailed presentation](https://bootlin.com/pub/conferences/2016/meetup/dbus/josserand-dbus-meetup.pdf) on D-Bus*
{.is-info}

* Export and enable a video backend, add support for OpenGL and peer-to-peer connection:

Does not display at the moment. 

SELinux needs to be disabled.

```
<graphics type="dbus"/>
	 <p2p value="on"/>
   <gl enable="yes"/>
</graphics>
```

It will look like that when launched: 

```
<graphics type="dbus" address="unix:path=/run/user/1000/libvirt/qemu/run/dbus/8-user-d-bus-dbus.sock">
  <gl enable="yes" rendernode="/dev/dri/renderD128"/>
</graphics>
```


* Export and enable an audio backend:

```
<graphics type="dbus">
  <audio id="1">
</graphics>
``` 


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



