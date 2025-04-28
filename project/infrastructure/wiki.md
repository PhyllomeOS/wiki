---
title: Wiki
description: 
published: true
date: 2025-04-28T16:23:02.638Z
tags: 
editor: markdown
dateCreated: 2025-04-28T16:15:31.727Z
---

# Wiki documentation

- [Wiki.js documentation on Cloudron](https://docs.cloudron.io/apps/wikijs/#git-storage)

## Set up

- From the Cloudron WebUI, open a terminal session inside the `wiki` container. Generate a SSH key pair inside this container and put in under `/app/data/`
- Log into with an admin account
- Go to to *Modules* -> *Storage* and select *Git*.
- Enable *SSH Private Key mod*, set SSH Private Key Path to `/app/data/ssh/id_rsa`.
