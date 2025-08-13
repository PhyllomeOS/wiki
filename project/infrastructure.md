---
title: Infrastructure
description: 
published: true
date: 2025-08-13T12:10:45.037Z
tags: 
editor: markdown
dateCreated: 2021-11-13T12:10:04.658Z
---

# The Project's Infrastructure

## Current solutions

| Function | Description | Location | 
| --- | --- | --- | --- |
| **PaaS** | [Cloudron.io](https://www.cloudron.io/) is used to deploy and keep up-to-date web applications needed by the project | https://my.phyllo.me |
| **Website** | [Grav](https://getgrav.org/) is used as a Content Management System (CMS)  | https://phyllo.me |
| **Git** | [Gitea](https://gitea.io/en-us/) is used to host repositories for projects | https://git.phyllo.me | 
| **Kan board** | [Wekan](https://wekan.github.io/) is used for issue tracking | https://kanboard.phyllo.me/ | 
| **Email** | [Rainloop](https://www.rainloop.net/) and the cloudron internal email server are used to provide email mailboxes for users |  https://mail.phyllo.me/ |
| **Wiki** | [Wiki.js](https://js.wiki/) is used to power the wiki  |  https://wiki.phyllo.me/ | 

## The Cloudron Platform-as-a-Service (PaaS)

- *Reverse DNS*: my.phyllome.org
- *Access*: SSH access via public key

### Domains

[Gandi](https://www.gandi.net/en-US) is the registrar.

- *Domains*: `phyllome.org` and `phyllo.me` are available
	- `phyllome.org` will eventually be used for production-ready services

### Server

A bare-metal is rented from [OVH](https://us.ovhcloud.com/)

### Hardware specifications

- *CPU*: Intel Xeon E3-1245v2 - 4c/8t - 3.4 GHz/3.8 GHz 
- *Memory*: RAM 32 GB 1333 MHz
- *Storage*: 2×480 GB SSD SATA, Soft RAID 0

### Software

- *Operating system*: Managed by Cloudron and based on Ubuntu Server 24.04 LTS.

## Website 

The webiste is powerd by Grav.

[Learn about Grav](http://learn.getgrav.org) 

## Wiki documentation

- [Wiki.js documentation on Cloudron](https://docs.cloudron.io/apps/wikijs/#git-storage)

### Set up

#### Git synchronization

The following allows for the Git repository `https://git.phyllo.me/roots/wiki` to be bilaterally synced with the wiki.

- From the Cloudron Web User Interface, open a terminal session inside the `wiki` container. 
- Generate an SSH key pair inside this container and put in under `/app/data/`
- Create a local repository path too, `mkdir /app/data/repo`
- Log into with an admin account
- Go to *Modules* > *Storage* and select *Git*.
- Under *Authentication Type*, select *ssh*
- Assuming the repository is hosted on git.phyllo.me and the *roots* organization, use `ssh://git@git.phyllo.me:29418/roots/wiki.git` under *Repository URI* 
- Under *Branch*, pick main
- Under *SSH Private Key Mode*, pick *path*
- Under *SSH Private Key Path*, pick `/app/data/id_rsa`
- Under *Default Author Name*, pick `lukas at phyllo me`
- Under *Default Author Name*, pick lukas
- Under Local Repository Path, pick */app/data/repo*
- Choose *Bidirectional* sync and then force sync to check if everything is working as expected.

#### Adding new users to the Editor group

New users coming from Cloudron can be automatically added to the Editor group.

To do so, 

- Navigate to *Administration* > *Authentication*. 
- Under *Active Strategies*, select Cloudron. 
- Under *Registration*, make sure that *Allow self-registration* is enabled and add the *Editors group* to the *Assign to group* field.
- It is also a good idea to add *phyllo.me* and *phyllome.org* to the *Limit to specific email domains* field.

## Git

- Two organizations:
	- Roots, for internally-developed projects
  - External, for external projects mirrored to the instance
- SSO for all Cloudron users
- Local root account
	- New password saved to lukas' password manager
  - TOTP 2FA enabled
- Application can be configured under `/app/data/app.ini` 
- Email domain allow list is enabled. See below for the configuration:

```
 root@container:/app/data# cat app.ini 
; Add customizations here - https://docs.gitea.io/en-us/config-cheat-sheet/

[security]
SECRET_KEY = [Hidden]

[service]
EMAIL_DOMAIN_ALLOWLIST=phyllo.me,phyllome.org
```

---

*[**Go to parent page**](https://wiki.phyllo.me/)*