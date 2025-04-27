---
title: Infrastructure
description: 
published: true
date: 2025-04-27T21:21:56.251Z
tags: 
editor: markdown
dateCreated: 2021-11-13T12:10:04.658Z
---

# Current infrastructure

## Platform-as-a-Service (PaaS)

* **Description**: [Cloudron.io](https://www.cloudron.io/) is used to deploy web applications consumed by the Phyllome OS project.
* **Location**: https://my.phyllo.me
* **Maintainer** : lukas at phyllo.me

Cloudron is hosted on a bare-metal server in OVH. an Ubuntu 24.04 virtual machine, on a Fedora Server 35 host.

Cloudron.io is a PaaS used to deploy and keep the web applications listed below up-do-date. It is our beloved single point-of-failure.

OpenLDAP is being used, so you can access most applications using a single account. Alas, there is no SSO, so the first time, you will have to log in into each application.

## Web applications

### Website

* **Description**: [Grav](https://getgrav.org/) is used as a Content Management System (CMS) 
* **Location**: https://phyllo.me
* **Maintainer**: lukas@phyllo.me
* **Access**: Core team only

Learn about Grav by checking out the dedicated [Learn Grav](http://learn.getgrav.org) site.

### Collaborative writing

* **Description**: [HedgeDoc](https://hedgedoc.org/) is used for collaborative writing 
* **Location**: https://docs.phyllo.me
* **Maintainer**: lukas@phyllo.me
* **Access**: Core team only

### File hosting

* **Description**: [Nextcloud](https://nextcloud.com/) is used for hosting files 
* **Location**: https://files.phyllo.me/
* **Maintainer**: lukas@phyllo.me
* **Access**: Core team only

#### Users

##### Webdav access

Replace `admin` by your username
Webdav access : https://files.phyllo.me/remote.php/dav/files/admin/

#### Administration

##### Enabled apps

Apps that were actively enabled post-installation:

* Default encryption module

##### Disabled apps

Apps that were actively disabled post-installation:

* Activity
* Auditing / Logging
* Collaborative tags
* Comments
* Contacts integration
* Dashboard
* External storage support
* Monitoring
* Nextcloud announcements
* Recommendations
* Talk
* Text
* Usage survey
* User Status
* Video player
* Weather status
* Federation
* Update notifications
* Support
* Password policy
* Log reader
* Notifications
* Photos

### Git

* **Description**: [Gitea](https://gitea.io/en-us/) is used as a backup for git repositories stored on Git 
* **Location**: https://git.phyllo.me
* **Maintainer**: lukas@phyllo.me
* **Access**: Core team only

### Issue tracking

* **Description**: [Wekan](https://wekan.github.io/) is used for issue tracking
* **Location**: https://kanboard.phyllo.me/
* **Maintainer**: lukas@phyllo.me
* **Access**: Core team only

### Mail

* **Description**: [rainloop](https://www.rainloop.net/) and the cloudron internal email server are used to provide email mailboxes for users
* **Location**: https://mail.phyllo.me/
* **Maintainer**: lukas@phyllo.me
* **Access**: Core team only

### Wiki

* **Description** : [Wiki.js](https://js.wiki/) is used to power the wiki 
* **Location** : https://wiki.phyllo.me
* **Maintainer** : lukas@phyllo.me

---

*[**Go to parent page**](https://wiki.phyllo.me/)*