---
title: Homepage
description: 
published: true
date: 2022-09-28T12:47:24.501Z
tags: 
editor: markdown
dateCreated: 2021-06-19T09:29:20.593Z
---

# The Phyllome OS wiki

`Welcome!`

*In this wiki, you will find guides about [how to install](/deploy/install), [use](/getstarted/disk) and [hack](/gofurther/hack) Phyllome OS. You will also find more generic information on the [underlying technologies](/virt), Phyllome OS [itself](/phyllomeos) and the surrounding [project](/project).*

> *For unauthenticated users, contributions are welcome using [Git](https://github.com/PhyllomeOS/wiki)*
> {.is-info}

Phyllome[^1] OS is an operating system that makes it easier to run [various operating systems](/gofurther) locally using [off-the-shelf hardware](/deploy/prepare) and [virtualization](/virt/lexicon#virtualization) technologies.

[^1]: According to [the Wiktionary](https://en.wiktionary.org/wiki/phyllome), Phyllome refers to the "foliar part of a plant; any organ homologous with a leaf, or [any organ] produced by metamorphosis of a leaf"

> *If you would rather avoid JavaScript altogether, or wish to download the content of this wiki locally, feel free to clone [this repository](https://github.com/PhyllomeOS/wiki).*
{.is-info}

> *This is the *alpha version* of this wiki.* 
> {.is-warning}

## Install the host Phyllome OS

*[This section](/deploy) illustrates how to install Phyllome OS on a compatible computer*

* [Is Phyllome OS right for you?](/deploy/rightforyou)
* [Prepare your computer](/deploy/prepare)
* [Create an installation medium](/deploy/medium)
* [Install from the installation medium](/deploy/install) (*default method*)
* [Post-installation configuration](/deploy/post-installation)

* ...and [**more**](https://wiki.phyllo.me/en/deploy)

## Deploy guests in the host

*[This section](/getstarted) describes how to deploy common operating systems within Phyllome OS*

* **Unix-like**
	* [Install](/gofurther/install-guest) a Linux guest system over the internet
	* [Automatically deploy](/gofurther/virt-install) an RPM-based guest system with `virt-install` and a kickstart file 

* **Windows NT**
  * [Install ReactOS](/gofurther/reactos)
  * [Install Windows 11 (*to be created*)](/gofurther/windows11)

* **Darwin-based**
  * [Install macOS (*to be created*)](/gofurther/macos)

* ...and [**more**](https://wiki.phyllo.me/en/getstarted#guest-operating-system-installations)

## Go further

*[This section](/gofurther#tasks_related_to_phyllome_os) illustrates specific tasks related to Phyllome OS.*

* [Use Phyllome as a live system](/getstarted/live) (*to test it*)
* [Perform a few checks](/gofurther/checks) on Phyllome OS
* [Resize an existing disk](/gofurther/resize)
* ...and [**more**](/gofurther)

## References

*[This section](/virt) provides information about technologies used by Phyllome OS.*

* [Guest support](/virt/guest)
* [Linux Kernel modules](/virt/host/modules) related to virtualization
* [Paravirtualized hardware](/virt/vm/virtio) (`virtio`)
* [Lexicon](/virt/lexicon) 
* ...and [**more**](/virt)

## About Phyllome OS

*[This section](/phyllomeos) describes the context around Phyllome OS and its design*. 

* [Context](/phyllomeos/context)
* [Purpose](/phyllomeos/purpose)
* [Use cases](/phyllomeos/use-cases)
* ...and [**more**](https://wiki.phyllo.me/en/phyllomeos)

### About the project

*[This section](/project) describes the project around Phyllome OS*.

* [How to contribute](/project/contribute)
* [How to join](/project/join)
* [Current infrastructure](/project/infrastructure)

### Public presence

* **The website**: https://phyllo.me
* **This wiki**: https://wiki.phyllo.me
* **The issue board**: [https://kanboard.phyllo.me](https://kanboard.phyllo.me/b/CH7qd98J2v7egmodk/development)
* **GitHub's repositories**: https://github.com/PhyllomeOS

