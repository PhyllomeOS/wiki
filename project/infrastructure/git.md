---
title: Git
description: 
published: true
date: 2025-04-27T22:36:19.893Z
tags: 
editor: markdown
dateCreated: 2025-04-27T22:29:08.400Z
---

# Git

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