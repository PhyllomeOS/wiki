---
title: Share an input device with a guest using evdev
description: 
published: true
date: 2024-05-15T19:20:21.209Z
tags: 
editor: markdown
dateCreated: 2022-08-13T00:26:02.801Z
---

# Share an input device

In this section, we'll explore how to share a locally attached input device with a guest virtual machine.

## With evdev

As of libvirt version 7.4.0, the [Linux evdev event interface](https://www.kernel.org/doc/html/latest/input/input.html?highlight=evdev#evdev) can be used to share an input device physically attached to the host with a guest, in a low-latency manner.

### Preparation

Before sharing an input device, follow these steps:

- List available input devices on your host system, excluding those containing `if` in their name, including those containing `event` in their name:

```
ls /dev/input/by-id/* | grep event | grep -v if
```

This command should output the names of eligible devices.

Example output:

```
/dev/input/by-id/usb-Corsair_CORSAIR_HARPOON_RGB_PRO_Gaming_Mouse_1902B02BAF5E04655DEB612AF5001C05-event-mouse
/dev/input/by-id/usb-Logitech_G513_RGB_MECHANICAL_GAMING_KEYBOARD_156930783132-event-kbd
/dev/input/by-id/usb-Logitech_USB_Keyboard-event-kbd
/dev/input/by-id/usb-Logitech_USB_Optical_Mouse-event-mouse
```

- Make sure that the correct one is selected by registering its inputs in your console:

```
cat /dev/input/by-id/usb-Logitech_G513_RGB_MECHANICAL_GAMING_KEYBOARD_156930783132-event-kbd
```

This step ensures you're working with the desired input device.

- Test the device by interacting with it on the host system. You should see gibberish characters displayed on your screen:

```
��c      $
��c���c���c�$��c�$��c׏��c׏��c                                             
```    

### Adding the input device to your virtual machine

- To share the input device with your virtual machine, add the following XML snippet to its domain definition (inside the <device> section):

```
<input type='evdev'>
      <source dev='/dev/input/by-id/usb-Logitech_G513_RGB_MECHANICAL_GAMING_KEYBOARD_156930783132-event-kbd' grab='all' repeat='on'/>
</input>
```

### Usage

Once the virtual machine is started, the input device will be captured by the guest system. 

> Press <kbd>Left Ctrl + Right Ctrl</kbd> simultaneously to switch your devices between the guest and the host.
{.is-info}


## Resources

* https://libvirt.org/formatdomain.html#input-devices

---

*[**Go to parent page**](https://wiki.phyllo.me/)*