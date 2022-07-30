---
title: Post-installation configuration
description: 
published: true
date: 2022-07-30T01:01:25.043Z
tags: 
editor: markdown
dateCreated: 2022-07-30T01:01:25.043Z
---

# Post-installation configuration

After Phyllome OS [has been successfully installed](/deploy/install) and [its first-launch process completed](/deploy/install#first-launch), a few tasks are required before it can be used to its fullest potential.

> As Phyllome OS evolves, the following post-installation configuration will, hopefully, be made obsolete 
{.is-info}

### Grant the current user the ability to manage system-based virtual machines

Any new user, including the one that has been created during the first-launch set up, won't be part of the `libvirt` group. It  means that it won't be able to manage the *qemu:///system*, which runs `libvirt` as root.

To avoid a password prompt each time you connect to *qemu:///system*, you can add the current user to the `libvirt` by using the following command, in the terminal:

```
sudo usermod -a -G libvirt $(whoami)
```

> Phyllome OS will eventually switch to the *qemu:///session* URI, which doesn't require elevated privileges. Have a look at [this great blog post](https://blog.wikichoon.com/2016/01/qemusystem-vs-qemusession.html) to understand some of the differences between the *session* and the *system* URI.  
{.is-info}

### Update GRUB and reboot

Unfortunately, the GRUB config won't correctly update during the kickstart phase, so it has to be done manually.

```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```
When the is done, please reboot: `sudo reboot`

### Modify the system allocated to the GPU in the BIOS/UEFI (vfio-mdev only)

> Some computers allow you to modify the system memory allocated or shared with the integrated GPU, which may allow you to create more vGPUs.
{.is-info}

> For Intel integrated graphics cards only; rarely available on laptops computers.
{.is-warning}

* Before the host operating system boots up, you need to enter the BIOS/UEFI and to look for a setting called *GPU aperture size*, or *GPU shared memory*. 

* Use the highest possible value.

> System memory will be reserved for the GPU, so make sure you have enough system memory to accomodate both the GPU and your operating system. 
{.is-warning}


---

*Are you looking for tasks to do with your system? If so, have a look at doing some [suggested tasks](/gofurther)*

[^1]: Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).