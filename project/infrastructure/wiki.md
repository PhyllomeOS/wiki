---
title: Wiki
description: 
published: true
date: 2025-04-28T17:08:02.543Z
tags: 
editor: markdown
dateCreated: 2025-04-28T16:15:31.727Z
---

# Wiki documentation

- [Wiki.js documentation on Cloudron](https://docs.cloudron.io/apps/wikijs/#git-storage)

## Set up

### Git synchronization

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

### Adding new users to the Editor group

New users coming from Cloudron can be automatically added to the Editor group.

To do so, 

- Navigate to *Administration* > *Authentication*. 
- Under *Active Strategies*, select Cloudron. 
- Under *Registration*, make sure that *Allow self-registration* is enabled and add the *Editors group* to the *Assign to group* field.
- It is also a good idea to add *phyllo.me* and *phyllome.org* to the *Limit to specific email domains* field.
