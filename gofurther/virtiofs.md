---
title: Share a host directory with a guest using virtiofs 
description: 
published: true
date: 2022-08-13T00:16:17.437Z
tags: 
editor: markdown
dateCreated: 2022-08-13T00:16:17.437Z
---

# virtio-fs

*to-be done*

* Memory backing needs to be added:

```
<domain type="kvm">
[...]
    <memoryBacking>
        <source type="memfb"/>
        <access mode="shared/>"
    </memoryBacking>
[...]
</domain>    
```

* Then a a directory can be shared using the following definition:

```    
<domain type="kvm">
[...]
    <devices>
    [...]
        <filesystem type="mount" accessmode="passthrough">
            <driver type="virtiofs"/>
            <source dir="/mnt/"> # Host directory to be shared with the guest
            <target dir="/mnt"/> # Directory on the guest
        </filesystem>
    [...]
    </devices>
[...]
</domain>    
```