---
title: Git
description: 
published: true
date: 2025-04-27T22:29:08.400Z
tags: 
editor: markdown
dateCreated: 2025-04-27T22:29:08.400Z
---

# Git

- SSO for all Cloudron users
- Local root account
	- New password saved to lukas' password manager
  - TOTP 2FA enabled
 - Email domain whitelist is enabled. See below for the configuration:
 
 ```
 root@container:/app/data# cat app.ini 
; Add customizations here - https://docs.gitea.io/en-us/config-cheat-sheet/

[security]
SECRET_KEY = [Hidden]

[service]
; Whether a new user needs to confirm their email when registering.
REGISTER_EMAIL_CONFIRM = true

#EMAIL_DOMAIN_WHITELIST=phyllo.me,phyllome.org
EMAIL_DOMAIN_ALLOWLIST=phyllo.me,phyllome.org
```