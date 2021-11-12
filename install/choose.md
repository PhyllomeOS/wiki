---
title: Choose
description: Understand if Phyllome OS is for you and pick the right version
published: true
date: 2021-11-12T09:04:10.130Z
tags: 
editor: markdown
dateCreated: 2021-11-11T18:18:23.807Z
---

# Is Phyllome OS right for you ?

Phyllome OS is based on two general assomptions: 

* **Virtual machines have become viable personnal computing environments** 
	* Due to their software-based nature, they can match or even exceed their physical counterparts in some areas. 
* **The host operating system should not be modified, in general**
	* Two Phyllome OS hosts should barely differ, allowing virtual machines to be fly from one host to the other.

## Limitations

Relying on a virtual machine as its primarily personnal environment has advantages but also comes with several limitations in comparaison to using a bare-metal operating system. Some limitations might be overcome one day, others might not. Let's list some of these limitations.

### Performance overhead

* Phyllome OS requires ressources to run, ressources that will not be accessible to guest operating systems.

### Guest performance

* Operating systems are often optimized to leverage hardware features that may not be accessible to an operating system installed on a virtual machine, or that would require specific developmments. In most cases, running a virtual machine instead of using the physical hardware directly will come with a performance penalty. This penalty might be greatly reduced by using some techniques, such as letting the virtual machine access the underlying hardware directly, but this particular solution is by definition not scalable to multiple virtual machines.

### Increased general complexity

* Instead of running just an operating system on top of some physical hardware, any Phyllome OS user would need to manage it as well as their primarly guest operating system. It might be more difficult for a user to troubleshoot an issue.     

### Lack of compatibility

* Phyllome OS relies on Linux drivers. 

## Requirements

`To be fetched from white paper`
