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

By default, `netboot.xyz.iso` should already be located under `/var/lib/libvirt/isos`. If it's not the case, please use the following command to fetch it, or navigate to [the website](https://netboot.xyz/):

```
wget https://boot.netboot.xyz/ipxe/netboot.xyz.iso -P /var/lib/libvirt/isos/
```
![post-install-conf-2.png](/assets/post-launch/post-install-conf-2.png)

## Access your virtual machine display

* Double-click on *my-first-live-vm* to open its virtual display, then click on *Connect to console*. 

![post-install-conf-3.png](/assets/post-launch/post-install-conf-3.png)

> Phyllome OS ships with a small ISO crafted by the team behind [netboot.xyz](https://netboot.xyz/), and that can do network boot, allowing it to do network-based installations of the most popular Linux distributions, among other niceties.
{.is-info}

![post-install-conf-11.png](/assets/post-launch/post-install-conf-11.png)

* After a few seconds, you will be greeted by the following screen.  

![post-install-conf-4.png](/assets/post-launch/post-install-conf-4.png)

* Under the menu, go to *View* and select *Full Screen* 

![post-install-conf-5.png](/assets/post-launch/post-install-conf-5.png)

* Go to *Live CDs*

> There is no disk attached to this virtual machine. As a result, only Live CDs will work out-the-box.
{.is-info}

![post-install-conf-10.png](/assets/post-launch/post-install-conf-10.png)

* Scroll down this list

![post-install-conf-13.png](/assets/post-launch/post-install-conf-13.png)

* Stop at *Tiny Core Linux* and press <kbd>Enter</kbd>

![post-install-conf-14.png](/assets/post-launch/post-install-conf-14.png)

* Select *Tiny Core Linux x86_64*

![post-install-conf-15.png](/assets/post-launch/post-install-conf-15.png)

* Select *Tiny Core Linux CorePure*

![post-install-conf-16.png](/assets/post-launch/post-install-conf-16.png)

* Enjoy your disposable virtual machine 

![post-install-conf-6.png](/assets/post-launch/post-install-conf-6.png)

* When you are done messing around, input the following, and you will be back in Phyllome OS

```
sudo poweroff
```

> That's it, congratulations! 
{.is-success}

---

*[**Go to parent page**](https://wiki.phyllo.me/)*