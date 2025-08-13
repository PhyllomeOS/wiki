---
title: Infrastructure
description: 
published: true
date: 2025-08-13T12:26:37.888Z
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
| **Email** | [Rainloop](https://www.rainloop.net/) and the Cloudron internal email server are used to provide email mailboxes for users |  https://mail.phyllo.me/ |
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

The website is powered by Grav.

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

## Gitea

- Two organizations:
	- Roots, for internally-developed projects
  - External, for external projects mirrored to the instance
- SSO for all Cloudron users
- Local root account
	- Password saved to lukas' password manager
  - TOTP 2FA enabled
- Application settings can be configured under `/app/data/app.ini`. See configuration [Cheat Sheet](https://docs.gitea.com/next/administration/config-cheat-sheet#actions-actions)
- Email domain allow list is enabled. See below for the configuration:

```
 root@container:/app/data# cat app.ini 
; Add customizations here - https://docs.gitea.io/en-us/config-cheat-sheet/

[security]
SECRET_KEY = [Hidden]

[service]
EMAIL_DOMAIN_ALLOWLIST=phyllo.me,phyllome.org
```

### Gitea runners

Two runners are available. One is using Docker, the other is running directly on a Fedora host.

#### Deploy a new runner

- Create a new virtual machine 
	- Optionaly install Docker
- Log to the machine
- Fetch latest runner binary: https://dl.gitea.com/act_runner/0.2.12/

For Linux running on amd64 CPU: 

```
curl https://dl.gitea.com/act_runner/0.2.12/act_runner-0.2.12-linux-amd64 --output act_runner
```
```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 19.2M  100 19.2M    0     0   102M      0 --:--:-- --:--:-- --:--:--  103M
```

- Add execute permission

```
chmod +x act_runner 
```

- Generate default configuration

```
./act_runner generate-config > config.yaml
```

- Modify the label name in the configuration file to allow for the runner to run directly on the host:

```
$ nano config.yaml 

# Example configuration file, it's safe to copy this as the default config file without any modification.

[...]
  labels:
    - "fedora-42:host"
[,..]

```

- Create a new instance-level runner by navigating to this page as the superadmin of the instance https://git.phyllo.me/-/admin/actions/runners/, and copy the token for the next step

- Then, on the host that will host the runner, use the following command:

```
./act_runner register --no-interactive --config config.yaml --instance https://git.phyllo.me --token <registration_token> --name fedora-host
```

For example, it would be 

```
/act_runner register --no-interactive --config /etc/act_runner/config.yaml --instance https://git.phyllo.me --token asdflkjlkajsfdfdsaadfsf --name fedora-host 
``` 

Then, run the runner: 

```
./act_runner daemon --config config.yaml
```


#### Documentation:

- Official documentation : https://docs.gitea.com/usage/actions/act-runner
- Act runner: https://gitea.com/gitea/act_runner/issues/380
- How can I exec on the host?: https://gitea.com/gitea/act_runner/issues/380
- Can I run gitea actions without docker?: https://stackoverflow.com/questions/76998107/can-i-run-gitea-actions-without-docker
- Self-hosting Git with CI/CD using Gitea - Part 2, Actions and Runners: https://thehomelabber.com/guides/self-hosted-git-ci-cd-part-2/
- Cannot (sometimes) find runner by label when multiple self-hosted runners are available #32348: https://github.com/go-gitea/gitea/issues/32348
- What is Gitea Runner: https://docs.gitea.com/runner/0.2.11/
- Gitea Actions - could not find runner by label #26045: https://github.com/go-gitea/gitea/issues/26045
- What workflow trigger events does Gitea support?: https://docs.gitea.com/next/usage/actions/faq#what-workflow-trigger-events-does-gitea-support
- Gitea Actions with Self-Hosted Gitea Runner: https://litts.me/projects/2024/second/
- Migrating from GitHub to Codeberg (Forgejo/Gitea): https://xrstf.de/notes/migrating-from-github-to-codeberg/

---

- Test worflow locally

```
./act_runner-0.2.12-linux-amd64 exec -W .gitea/workflows/checkout-fedora.yml 
```





---

*[**Go to parent page**](https://wiki.phyllo.me/)*