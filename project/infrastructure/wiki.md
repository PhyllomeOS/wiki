---
title: Wiki
description: 
published: true
date: 2025-04-28T16:48:19.667Z
tags: 
editor: markdown
dateCreated: 2025-04-28T16:15:31.727Z
---

# Wiki documentation

- [Wiki.js documentation on Cloudron](https://docs.cloudron.io/apps/wikijs/#git-storage)

## Set up

- From the Cloudron WebUI, open a terminal session inside the `wiki` container. Generate a SSH key pair inside this container and put in under `/app/data/`
- Create a local repository path too, `mkdir /app/data/repo`
- Log into with an admin account
- Go to to *Modules* -> *Storage* and select *Git*.
- Under *Authentication Type*, select *ssh*
- Assuming the repository is hosted on git.phyllo.me and the roots organizsation, use `ssh://git@git.phyllo.me:29418/roots/wiki.git` under *Repository URI* 
- Under *Branch*, pick main
- Under *SSH Private Key Mode*, pick *path*
- Under *SSH Private Key Path*, pick `/app/data/id_rsa`
- Under *Default Author Name*, pick `lukas at phyllo me`
- Under *Default Author Name*, pick lukas
- Under Local Repository Path, pick */app/data/repo*
- Choose *Bi-directionnal* sync and then force sync to check if everything is working as expected.

