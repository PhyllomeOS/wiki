---
title: Netboot for all
description: 
published: true
date: 2021-11-25T13:58:10.457Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:43:58.697Z
---

# Use a live guest OS

As of now, `netboot.xyz` is one of the main way to deploy or use a guest operating system inside Phyllome OS. It is compatible with most (but not all) guest operating systems. This small guide will show you how to deploy a live system inside Phyllome OS.

## Preparation

By default, `netboot.xyz.iso` should already be located under `var/lib/libvirt/iso`. If it's not the case, please use the following command to fetch it, or navigate to [the website](https://netboot.xyz/):

```
wget https://boot.netboot.xyz/ipxe/netboot.xyz.iso -P /var/lib/libvirt/iso/
```

## Run the script

The following script, which also doesn't require root privileges, will create a virtual machine called `my-first-live-vm`. This virtual machine will be started automatically and added to `virt-manager`.

```
/usr/sbin/create-live-vm.sh
```
*Notice the new icon under QEMU/KVM: this is the new virtual machine that has just been created. Go to the section to learn how to interact with it.*

![post-install-conf-2.png](/post-launch/post-install-conf-2.png)

## Access your virtual machine display

* Double-click on *my-first-live-vm* to open its virtual display, then click on *Connect to console*. 

![post-install-conf-3.png](/post-launch/post-install-conf-3.png)

> Phyllome OS ships with a small ISO crafted by the team behind [netboot.xyz](https://netboot.xyz/), and that can do network boot, allowing it to do network-based installations of the most popular Linux distributions, among other niceties.
{.is-info}

![post-install-conf-11.png](/post-launch/post-install-conf-11.png)

* After a few seconds, you will be greeted by the following screen.  

![post-install-conf-4.png](/post-launch/post-install-conf-4.png)

* Under the menu, go to *View* and select *Full Screen* 

![post-install-conf-5.png](/post-launch/post-install-conf-5.png)

* Go to *Live CDs*

> There is no disk attached to this virtual machine. As a result, only Live CDs will work out-the-box.
{.is-info}

![post-install-conf-10.png](/post-launch/post-install-conf-10.png)

* Scroll down this list

![post-install-conf-13.png](/post-launch/post-install-conf-13.png)

* Stop at *Tiny Core Linux* and press <kbd>Enter</kbd>

![post-install-conf-14.png](/post-launch/post-install-conf-14.png)

* Select *Tiny Core Linux x86_64*

![post-install-conf-15.png](/post-launch/post-install-conf-15.png)

* Select *Tiny Core Linux CorePure*

![post-install-conf-16.png](/post-launch/post-install-conf-16.png)

* Enjoy your disposable virtual machine 

![post-install-conf-6.png](/post-launch/post-install-conf-6.png)

* When you are done messing around, input the following, and you will be back in Phyllome OS

```
sudo poweroff
```

> That's it, congratulations! 
{.is-success}

---

*Are you looking for other tasks to execute on your system? If so, go the [suggested tasks section](/gofurther)*

