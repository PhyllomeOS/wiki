---
title: Share a host directory with a guest using virtiofs 
description: 
published: true
date: 2023-02-02T19:05:40.611Z
tags: 
editor: markdown
dateCreated: 2022-08-13T00:16:17.437Z
---

# Sharing a directory 

> For KVM/QEMU, as of January 2023, virtio-fs is only available for virtual machines managed by the system libvirt instance (`qemu:///system`)
{.is-warning}

> As of January 2023, virtio-fs does not support read-only mode, meaning a guest will be able to write to the host's folder.
{.is-warning}

[Virtio-fs](https://virtio-fs.gitlab.io/), shorts for virtio shared filesystem, allows for a directory located on the host to be shared with a guest. 

It is designed to be fast and optimized for local usage, when the host and the guest are located on the same physical machine. 

Just as with other virtio devices, it requires specialized drivers to be written for the guest operating system.

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
            <source dir="/opt/share"> # The host directory to be shared with the guest
            <target dir="share"> # The target dir value refers to the tag used inside the guest to describe the share.
        </filesystem>
    [...]
    </devices>
[...]
</domain>    
```

### Mount the folder inside the guest

* Inside the guest VM, mount the folder using the following command to mount the `/mnt` host directory on the guest, using also the `/mnt` point: 

`# mount -t virtiofs share /mnt/`

## Resources

* Official website: https://virtio-fs.gitlab.io/index.html#status
* In the context of a Windows guest: https://github.com/virtio-win/kvm-guest-drivers-windows/wiki/VirtIO-FS:-Shared-file-system
* https://wiki.archlinux.org/title/Libvirt#Sharing_data_between_host_and_guest

