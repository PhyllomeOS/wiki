---
title: Security in Phyllome OS
description: 
published: true
date: 2022-01-31T12:50:53.781Z
tags: 
editor: markdown
dateCreated: 2022-01-31T12:35:54.544Z
---

# Security in Phyllome OS

> *Phyllome OS is currently in alpha stage. It should not be used to store any sensitive data*
{.is-warning}

Phyllome OS is a Fedora Remix and as such directly inherits every single security measures in place for Fedora-related distributions, such as SELinux. It also brings some unique security-related features.

* **List of unique security-related features**
	* Unprivileged virtual machines with `qemu:///session`, by default
	* Filesystem-level encryption with `fscrypt`
  * Minimal installations
* **Planned features**
	* Unattended installation of security updates
  * `systemd` hardening
  * `gnome-shell` hardening

## Features

### Data at-rest encryption

Currently, Phyllome OS does **not** provide any kind of encryption by default at the host level. 

It provides early support for Filesystem-level encryption, which is just one line of defense. 

For any virtual disks that will contain personal data, users are strongly advised to use full-disk encryption as provided by their guest operating system.




---

*[**Go back to parent page**](/phyllomeos)*