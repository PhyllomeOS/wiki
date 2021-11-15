---
title:  Checkbox your system
description: 
published: true
date: 2021-11-15T12:00:04.914Z
tags: 
editor: markdown
dateCreated: 2021-11-13T10:47:33.615Z
---

# Prepare the host computer

## Requirements

`To-do`

These instructions are valid for x86-64 computers that do ship with Linux or Windows

> As of now, Phyllome OS only officially supports host computers with Intel CPUs and Intel internal graphics card (iGPU). Other editions will follow.
{.is-warning}

## Enable hardware-assisted virtualization

For Phyllome OS to work as intended, hardware-assisted virtualization needs to be enabled. 

> For Apple hardware, support for hardware-assisted virtualization seems to depend on you firmware version and your CPU model. Go directly to the `Make sure that hardware-assisted virtualization is enabled` section.
{.is-info}

### Access the firmware

During the boot process, you need to press a certain key to access the firmware configuration tool for your motherboard, also known as BIOS or UEFI. 

The most common keystrokes are <kbd>F2</kbd> or <kbd>Del</kbd>.

Hardware manufacturers could not agree on a common keystroke to access the firmware configuration tool, so please have a look at the documentation provided by your hardware manufacturer.

* **Windows-based computers**


### Modify the firmware configuration


*Now that you are done, you can go to the next section to [create an installation medium](/deploy/medium).*


### Make sure that hardware-assisted virtualization is enabled 



