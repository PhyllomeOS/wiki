---
title: Understand what you are signing up for
description: 
published: true
date: 2022-01-07T11:17:56.025Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:19:38.215Z
---

# Is Phyllome OS right for you?

## Phyllome OS Philosophy

> Phyllome OS has one primarly goal: *to let users bring their favorite operating system and to run them well*.

* The host, Phyllome OS, is designed to be as discrete as possible.
* Phyllome OS should mostly take care of itself. 
* Eventually, users should be able to reach *the state of virtual enlightenment*, which boils down to:
	* Accepting the fact that your favorite operating system is running inside a virtual machine
  * Learning how to leverage this new state of affairs.

> Phyllome OS has just started its journey and there is still a long, *years-long*, way to go to achieve its vision. 
It has several, [significative limitations](/phyllomeos/cons-and-pros), so make sure you understand them; depending on what you wish to achieve, you may instead prefer [to favor other operating systems](https://wiki.phyllo.me/en/phyllomeos/comparaison); [support](/virt#guests) for guest systems differs widely. 
{.is-warning}

## Phyllome OS Desktop and Phyllome OS Server 

Phyllome OS exists in two main versions: 

* **Phyllome OS Desktop**, which features a graphical desktop environment. 
* **Phyllome OS Server**, which does not feature a graphical desktop environment (also known as headless)

> Phyllome OS Server is made for power users. It includes all virtualization enhancements that Phyllome OS Desktop provides, minus the Desktop Environment. If you don't know which one to choose, you should probably pick the Desktop version. 
{.is-info}

Phyllome OS Desktop and Phyllome OS Server also comes with several editions optimized for a particular combination of hardware.

> As of now, **only Phyllome OS Desktop II is officially supported**. A computer with both an Intel CPU and an Intel GPU is needed to leverage Phyllome OS. Support for other other editions are expected for the Beta realease.  
{.is-info}

|  | GPU-agnostic | Intel GPUs | AMD GPUs |
|---|---|---|---|
| *Intel CPU* | N/A | Phyllome OS Desktop II | Phyllome OS Desktop IA |
| *AMD CPU* | N/A | Phyllome OS Desktop AI  | Phyllome OS Desktop AA |
| CPU-agnostic | Phyllome OS Desktop | N/A  | N/A |

Depending on your hardware, you need to pick the right edition. For example, if you possess an Intel CPU and an AMD graphics card, you should pick either Phyllome OS Desktop IA or Phyllome OS Server IA.

---

*Please go to [the next section](/deploy/prepare) to prepare your host computer.*

