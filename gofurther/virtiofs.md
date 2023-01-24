---
title: Share a host directory with a guest using virtiofs 
description: 
published: true
date: 2023-01-24T16:27:16.582Z
tags: 
editor: markdown
dateCreated: 2022-08-13T00:16:17.437Z
---

# Sharing a directory 

> *As of January 2023, virtio-fs is only available for virtual machines managed by the system libvirt instance (`qemu:///system`)*
{.is-info}

> *As of January 2023, virtio-fs does not feature a read-only mode. Do not share a host directory with a untrusted guest*.
{.is-warning}

[Virtio-fs](https://virtio-fs.gitlab.io/), shorts for virtio shared filesystem, allows you to share a directory located on the host with a guest. It is designed to be fast and optimized for local usage, when the host and the guest are located on the same physical machine. 

## The guest

### Edit XML configuration

* Memory backing needs to be added to the XML definition:

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

* A filesystem device has to be added.

```    
<domain type="kvm">
[...]
    <devices>
    [...]
        <filesystem type="mount" accessmode="passthrough">
            <driver type="virtiofs"/>
            <source dir="/mnt/"> # The host directory to be shared with the guest
            <target dir="share"/> # Contrary to what the name implies, this is the tag used inside the guest
        </filesystem>
    [...]
    </devices>
[...]
</domain>    
```

### Mount the folder inside the guest

* Inside the guest VM, mount the folder using the following commmand to mount the `/mnt` host directory on the guest, using also the `/mnt` point: 

`# mount -t virtiofs share /mnt/`

## Resources

* Official website: https://virtio-fs.gitlab.io/index.html#status
* In the context of a Windows guest: https://github.com/virtio-win/kvm-guest-drivers-windows/wiki/VirtIO-FS:-Shared-file-system

