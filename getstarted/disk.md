---
title: Get started with Phyllome OS
description: 
published: true
date: 2021-11-23T15:56:24.591Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:37:31.498Z
---

# How to use Phyllome OS

*This section explains how to further configure Phyllome OS, and how to deploy a tiny and live operating system within it.*   

## Post-installation configuration

After Phyllome OS [has been successfully installed](/deploy/install) and [its first-launch process completed](/deploy/install#first-launch), a few tasks are required before it can be used to its fullest potential.

> As Phyllome OS evolves, one of the main goal is to shorten the time it would take for an end-user to have a fully operational virtual machine loaded with the installer of their favorite operating system, to the point that a user may not see the Phyllome OS environment
at all.
{.is-info}

> The following post-installation configuration will, hopefully, be made obsolete in a future Phyllome OS version. 
{.is-info}

### Grant the current user the ability to manage virtual machines

Any new user, including the one that has been created during the first-launch set up, won't be part of the `libvirt` group. It  means that it won't be able to manage the *qemu:///system*, which runs `libvirt` as root.

To avoid a password prompt each time the Virtual Machine Manager is launched, you can add the current user to the `libvirt` by using the following command, in the terminal:

```
sudo usermod -a -G libvirt $(whoami)
```
> A known bug affects the terminal: extra spaces between letters. To solve it, click on the burger menu (the three stacked horizontal lines) then go to *Preferences > Profiles > Unnamed* and check the box called *Custom font*. 
{.is-warning}

> Phyllome OS will eventually switch to the *qemu:///session* URI, which doesn't require elevated privileges. Have a look at [this great blog post](https://blog.wikichoon.com/2016/01/qemusystem-vs-qemusession.html) to understand some of the differences between the *session* and the *system* URI.  
{.is-info}

### Run a few scripts

During the installation process, [a few scripts are fetched](https://github.com/PhyllomeOS/phyllomeos/tree/main/post) and stored under the `/usr/sbin` directory. They need to be run to further customize Phyllome OS.

#### Desktop enhancements

The following script will change the desktop background and pick opinionated defaults for the Virtual Machine Manager. It will also add a new User session URI for the Virtual Machine Manager. 

Open the terminal and run the following script as a regular user:

```
/usr/sbin/configure-vmm-and-desktop.sh
```
*The updated desktop background. Notice that there is now a new URI called QEMU/KVM User session*

![post-install-conf-1.png](/post-launch/post-install-conf-1.png)

#### Create and run a virtual machine without any attached disk

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

When you are done messing around, input the following, and you will be back in Phyllome OS

```
sudo poweroff
```

> That's it, congratulations! 
{.is-success}

---

*Are you looking for tasks to do with your system? If so, have a look at doing some [suggested tasks](/gofurther)*

[^1]: Although, we very much encourage you to [hack it](https://github.com/PhyllomeOS/phyllomeos#how-to-hack-phyllome-os).