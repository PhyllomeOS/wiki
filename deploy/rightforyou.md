---
title: Understand what you are signing up for
description: 
published: true
date: 2022-01-07T14:29:05.401Z
tags: 
editor: markdown
dateCreated: 2021-11-13T11:19:38.215Z
---

# Is Phyllome OS right for you?

## Phyllome OS Philosophy

> Phyllome OS has one primarly goal: *to let users bring their favorite operating system and to run them well*.

* The host operating system, Phyllome OS, is designed to be as discrete as possible.
* Phyllome OS should mostly take care of itself. 
* Eventually, users should be able to reach *the state of virtual enlightenment*, which boils down to:
	* Accepting the fact that your favorite operating system is running inside a virtual machine.
  * Learning how to leverage this new state of affairs.

> Phyllome OS has just started its journey and there is still a long, *years-long*, way to go to achieve its vision. 
It has several [significative limitations](/phyllomeos/cons-and-pros), so make sure you understand them; depending on what you wish to achieve, you may instead prefer [to favor other operating systems](https://wiki.phyllo.me/en/phyllomeos/comparaison); finally, [support](/virt#guests) for guest systems differs widely. 
{.is-warning}

## Phyllome OS Desktop and Phyllome OS Server 

Phyllome OS exists in two main versions: 

* **Phyllome OS Desktop**, which features a graphical desktop environment. 
* **Phyllome OS Server**, which does not feature a graphical desktop environment.

> Phyllome OS Server is made for power users. It includes all virtualization enhancements that Phyllome OS Desktop provides, minus the Desktop Environment. If you don't know which one to choose, you should most certainly pick the Desktop version. 
{.is-info}

Phyllome OS Desktop and Phyllome OS Server also comes with several editions optimized for a particular combination of hardware. At some point, there will be merged into one.

> As of now, **only Phyllome OS Desktop II is officially supported**. A computer with both an Intel CPU and an Intel GPU (gen 5th to gen 9th) is expected, so it can leverage most features Phyllome OS can offer. Support for other other editions are expected for the Beta realease.  
{.is-info}

|  | GPU-agnostic[^1] | Intel GPUs[^2] |
|---|---|---|---|
| *Intel CPU* | **Phyllome OS Desktop I** and **Phyllome OS Server I** | **Phyllome OS Desktop II** and **Phyllome OS Server II** | 
| *AMD CPU* | **Phyllome OS Desktop A** and **Phyllome OS Server A** | N/A  |
| CPU-agnostic | **Phyllome OS Desktop** and **Phyllome OS Server** | N/A  |

[^1]: GPUs agnostic editions will work with almost any GPUs that Linux can drive. Some severe limitations apply to [most recent Nvidia offerings](https://nouveau.freedesktop.org/FeatureMatrix.html). In general, **Nvidia GPUs are strongly discouraged** in all capacities, at least until Nvidia stop actively hindering the development of open-source drivers for its GPUs.
[^2]: Only [Broadwell-based SoC](https://en.wikipedia.org/wiki/Broadwell_(microarchitecture)) (5th generation) to [Cascade Lake-based SoC](https://en.wikipedia.org/wiki/Cascade_Lake_(microarchitecture)) (9th generation) are supported. If you possess a more recent SoC from Intel, for instance one based on the Tiger Lake SoC, please pick Phyllome OS Desktop I or Phyllome OS Desktop instead.

---

*Ready to try it out? If soplease go to [the next section](/deploy/prepare) to prepare your host computer.*

