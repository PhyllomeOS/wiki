---
title: Share a host directory with a guest using virtiofs
description: 
published: true
date: 2025-04-28T22:45:21.257Z
tags: 
editor: markdown
dateCreated: 2022-08-13T00:16:17.437Z
---

# Sharing a directory between the host and the guest 

## Virtio-fs in a nutshell

[Virtio-fs](https://virtio-fs.gitlab.io/), shorts for *Virtio shared FileSystem*, allows for a directory located on the host to be shared with a guest. 

It is designed to be fast and optimized for local usage, when the host and the guest are located on the same physical machine. It is therefore a perfect fit for Phyllome OS. 

Just as with other `virtio` devices, `virtio-fs` requires specialized drivers to be written for the host and the guest operating system.

## Guest configuration

> For KVM/QEMU, as of January 2023, virtio-fs is only available for virtual machines managed by the system libvirt instance (`qemu:///system`)
{.is-warning}

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

* Add the filesystem device to the guest. In this the following case, the directory `/opt/share/` will be shared with the guest:

```    
<domain type="kvm">
[...]
    <devices>
    [...]
        <filesystem type="mount" accessmode="passthrough">
            <driver type="virtiofs"/>
            <source dir="/opt/share"> # The host directory to be shared with the guest
            <target dir="share"> # The target dir value refers to the mount tag used inside the guest, not the target dir inside the guest
        </filesystem>
    [...]
    </devices>
[...]
</domain>    
```

### Mount the folder inside the guest

* Inside the guest VM, mount the folder using the following command to mount the `/opt/share` host directory to the guest, using also the `/mnt` point: 

```
# mount -t virtiofs share /mnt/
```

* To make it permanent, add the following line to `/etc/fstab`:

```
share /mnt/ virtiofs rw,noatime,_netdev 0 2
```

* Make sure it works before rebooting the guest virtual machine, by unmounting the share and reloading the `systemd` daemon`

```
# umount /mnt/ && systemctl daemon-reload
```

* and then mounting all share available in `fstab`:

```
# mount -all
```

## Resources

* Official website: https://virtio-fs.gitlab.io/index.html#status
* In the context of a Windows guest: https://github.com/virtio-win/kvm-guest-drivers-windows/wiki/VirtIO-FS:-Shared-file-system
* https://wiki.archlinux.org/title/Libvirt#Sharing_data_between_host_and_guest

---

*[**Go to parent page**](https://wiki.phyllo.me/)*