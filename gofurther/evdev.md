---
title: Share an input device with a guest using evdev
description: 
published: true
date: 2022-08-13T00:26:02.801Z
tags: 
editor: markdown
dateCreated: 2022-08-13T00:26:02.801Z
---

# Sharing an input device with a guest

## evdev XML conf.

```
<input type='evdev'>
      <source dev='/dev/input/by-path/platform-i8042-serio-1-event-mouse/'>
</input>
<input type='evdev'>
      <source dev='/dev/input/by-path/platform-i8042-serio-0-event-kbd' grab='all' repeat='on'/>
</input>
```