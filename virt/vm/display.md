---
title: Display
description: How to access a virtual machine's display
published: true
date: 2023-10-15T15:11:00.161Z
tags: 
editor: markdown
dateCreated: 2022-07-31T09:22:05.854Z
---

# Display

A virtual display can be attached to a virtual machine. It is a must-have for non-headless scenarios.

## Display types

### SDL display

The [Simple DirectMedia Layer](https://www.libsdl.org/) (SDL)-powered display is a local-only low-latency display. 

> The SDL display is only avalable with virtual machines created using the QEMU/KVM **User Session**.
{.is-info}

> Mouse grab does not currently work with the SDL display
{.is-warning}

> The display resolution of your guest display should not exceed that of your physical screen
{.is-info}

#### SELinux-related configuration

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

#### SDL XML configuration

* The default display can be identified using `echo $DISPLAY`. 

``` 
$ echo $DISPLAY
:0
```

The same applies to `xauth`. On Wayland, it would look like that. 

``` 
$ echo $XAUTHORITY
/run/user/1000/.mutter-Xwaylandauth.ARIY51
```

* Example of an XML SDL configuration, with OpenGL enabled. This example requires a 3D-capable graphic card to be attached to the guest computer, such as `virtio-gpu`.

```
<graphics type="sdl" display=":0" xauth="/run/user/1000/.mutter-Xwaylandauth.ARIY51" fullscreen="yes">
  <gl enable="yes"/>
</graphics>
```

> The fullscreen attribute is not honored at the moment
{.is-warning}

### D-Bus display

[D-Bus](https://www.freedesktop.org/wiki/Software/dbus/) is a desktop-oriented middleware that can be used to create a display for a virtual machine.  

#### Libvirt

* Add a D-Bus video backend and add enable for OpenGL:

```
<graphics type="dbus">
  <gl enable="yes"/>
</graphics>
```

> This equates to `-display dbus,gl=on` in QEMU
> 
{.is-info}

When the virtual machine is launched, a specific D-Bus address will be choosen, as well as a rendering device: 

```
<graphics type="dbus" address="unix:path=/run/user/1000/libvirt/qemu/run/dbus/8-user-d-bus-dbus.sock">
  <gl enable="yes" rendernode="/dev/dri/renderD128"/>
</graphics>
```

* Add a D-Bus audio backend:

```
<graphics type="dbus">
  <audio id="1">
</graphics>
```

#### Connect to the D-Bus display

A third-party tool is required to interact to the D-Bus display. 

[Libmks](https://gitlab.gnome.org/GNOME/libmks), which is under development, is such a tool. 

> Due to [a bug](https://gitlab.gnome.org/GNOME/libmks/-/issues/16), it is currenlty only possible to connect a D-Bus display with plain QEMU
{.is-warning}

Libmks has to be built from source.

- Clone the repository 

``` 
git clone https://gitlab.gnome.org/GNOME/libmks
``` 

- Change directory

```
cd libmks
```

- Build it

``` 
meson setup build
cd build
ninja
```

- Launch a diskless virtual machine

```
qemu-system-x86_64 \
  -enable-kvm \
  -machine q35 \
  -drive if=pflash,format=raw,readonly=on,file=/usr/share/edk2-ovmf/x64/OVMF_CODE.fd \
  -cpu host \
  -device virtio-vga-gl \
  -m 4G \
  -smp 2,sockets=1,dies=1,cores=2,threads=1 \
  -display dbus,gl=on \
  -device virtio-tablet-pci \
  -device virtio-keyboard-pci \
```

- From another terminal tab or window, launch the previously built MKS using the following command 

```
./build/tools/mks
```

As there is no Live ISO or disk attached to the virtual machine, you will eventually land in the UEFI shell. 

## Resources

* [Detailed presentation](https://bootlin.com/pub/conferences/2016/meetup/dbus/josserand-dbus-meetup.pdf) on D-Bus
* [Official resource](https://libvirt.org/formatdomain.html#graphical-framebuffers) for libvirt-compatible displays, including various XML examples
* [Libmks](https://gitlab.gnome.org/chergert/libmks) provides a "Mouse, Keyboard, and Screen" to QEMU using the D-Bus device support in QEMU and GTK 4. 
* [QEMU D-Bus display experiment](https://gitlab.com/marcandre.lureau/qemu-display/) is a WIP Rust crates to interact with a -display dbus QEMU
* [SDL graphics](https://fedoraproject.org/wiki/How_to_debug_Virtualization_problems#SDL_Graphics)

---

*[**Go to parent page**](https://wiki.phyllo.me/)*