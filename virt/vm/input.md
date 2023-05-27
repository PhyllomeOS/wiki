---
title: Input devices
description: How to share input devices with a virtual machine
published: true
date: 2022-08-02T09:59:31.526Z
tags: 
editor: markdown
dateCreated: 2022-08-01T10:42:14.864Z
---

# Input devices

Input devices such as keyboards and mice are a must to directly interact with a virtual machine. There are multiple ways to share an input device with your virtual machine.

## Summary

* *to-be done. Add table here*.

## Methods

### Evdev

Event devices (evdev) is a generic input event interface available in the [Linux](https://www.kernel.org/doc/Documentation/input/input.txt) and FreeBDS kernels. 

* Identify available input devices under `/dev/input/by-path/` or `/dev/input/by-id/` and look for devices that contains the string *event* in their name.

```
ls /dev/input/*
```
```
/dev/input/by-path:
pci-0000:07:00.0-event-mouse  
pci-0000:09:00.0-mouse
pci-0000:07:00.0-mouse        platform-i8042-serio-0-event-kbd
pci-0000:08:00.0-event-kbd    platform-i8042-serio-1-event-mouse
pci-0000:09:00.0-event-mouse  platform-i8042-serio-1-mouse
```

* Check if it's the correct device using the following command and typing or clicking on your device

```
sudo cat /dev/input/by-path/pci-0000:08:00.0-event-kbd
```

* If gibberish symbols appear on your console as you type, it means that the device has been correctly identified, and that you can <kbd>Ctrl+Z</kbd>

```
��b����b����b�!��b���b�� ��b����b����b����b����b��fdsa��b�( ��b�(��b!��b��bR��bR��bW��bW��b�!��b�f��b4 ��b4��bV��bV��bX��bXdsa��b!:	!��b!:	��b>:	 ��b>:	��b�
��b�
��b�y
��b�y
```

Edit the virtual machine's definition and replace `MOUSE_NAME` and `KEYBOARD_NAME` with the previously identified devices. 

```
<input type="evdev">
  <source dev="/dev/input/by-path/MOUSE_NAME"/>
</input>
<input type="evdev">
  <source dev="/dev/input/by-path/KEYBOARD_NAME" grab="all" repeat="on"/>
</input>
```

* In-depth [Passthrough Post article](https://passthroughpo.st/using-evdev-passthrough-seamless-vm-input/) about evdev. 

---

*[**Go to parent page**](https://wiki.phyllo.me/)*
