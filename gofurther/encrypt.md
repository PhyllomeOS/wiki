---
title: Encrypt the directory that contains virtual disk images
description: 
published: true
date: 2022-01-31T12:30:06.985Z
tags: 
editor: markdown
dateCreated: 2022-01-31T12:30:06.985Z
---

# Encrypt virtual disk images

> *Integration of filesystem-level encryption in Phyllome OS is a work-in-progress*
{.is-warning}

## Context

At the moment, Phyllome OS does **not** provide any kind of encryption by default at the host level. Filesystem-level encryption is just one layer of protection. For any virtual disks that contains personnal data, users are strongly advised to use full disk encryption as provided by their guest operating system.

This guide will show you how to compile [^1] and configure `fscrypt` to encrypt virtual disk images. It will also show you how to configure [PAM](http://www.linux-pam.org/) to work alongside `fscrypt`

[^1]: *As of now, `fscrypt` does not ship as an RPM package*

> *[`fscrypt`](https://github.com/google/fscrypt) provides filesystem-level encryption and its library [is part](https://www.kernel.org/doc/html/v4.18/filesystems/fscrypt.html) of the Linux kernel. It is widely used by Android-based devices, but only compatible with a handful of filesystems*
{.is-info}

> *`fscrypt` does **not** support in-place encryption. Only previously empty directories can be encrypted. If you wish to encrypt a directory which already contains files, move these files outside of the directory, encrypt it, and put the files back in* 
{.is-warning}

## Installation

### Building from source

* Install dependencies to compile `fscrypt`:

```
sudo dnf install -y git golang pam-devel m4 authselect
```

* Fetch the source code:

```
go get -d github.com/google/fscrypt/...
```

* Move to the install folder:

```
cd ~/go/pkg/mod/github.com/google/fscrypt\@v0.3.1/
```

> If a new version is released, for instance `v0.3.2`, update the above path accordingly
{.is-info}

* Run `make install`, which will install `fscrypt` to `/usr/local/bin`, `pam_fscrypt.so` to `/usr/local/lib/security`, and `pam_fscrypt/config` to `/usr/local/share/pam-configs`.*

```
sudo make install

fatal: not a git repository (or any of the parent directories): .git
install -d /usr/local/bin
install bin/fscrypt /usr/local/bin
install -d /usr/local/lib/security
install bin/pam_fscrypt.so /usr/local/lib/security
m4 --define=PAM_INSTALL_PATH=/usr/local/lib/security/pam_fscrypt.so < pam_fscrypt/config > bin/config
install -d /usr/local/share/pam-configs
install bin/config /usr/local/share/pam-configs/fscrypt
install -Dm644 cmd/fscrypt/fscrypt_bash_completion /usr/local/share/bash-completion/completions/fscrypt
```

> The error message seems innocuous
{.is-info}

* Move `pam_fscrypt.so` to `/usr/lib64/security/`, where it belongs:

```
sudo mv /usr/local/lib/security/pam_fscrypt.so /usr/lib64/security/pam_fscrypt.so
``` 

### Setup

* Identify the `root` partition (`/`) using the command line utility `lsblk`:

`lsblk`

``` 
[groot@phyllome ~]$ lsblk
NAME                                       MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINTS
zram0                                      251:0    0  7.8G  0 disk  [SWAP]
nvme0n1                                    252:0    0   50G  0 disk  
├─nvme0n1p1                                252:1    0  128M  0 part  /boot/efi
├─nvme0n1p2                                252:2    0  384M  0 part  /boot
└─nvme0n1p3                                252:3    0 49.5G  0 part  /
```

In this case, it is `nvme0n1p3` but valid value may be `sda3` or `vda3` or `system-root` for LVM-based systems

* Activate `tune2fs` by providing the absolute path to the root partition:

```
sudo tune2fs -O encrypt /dev/nvme0n1p3

tune2fs 1.45.6 (20-Mar-2020)
```

* Verify proper activation:

```
sudo zgrep -h ENCRYPTION /boot/config-$(uname -r) | sort | uniq

CONFIG_BLK_INLINE_ENCRYPTION=y
CONFIG_BLK_INLINE_ENCRYPTION_FALLBACK=y
CONFIG_FS_ENCRYPTION_ALGS=y
CONFIG_FS_ENCRYPTION_INLINE_CRYPT=y
CONFIG_FS_ENCRYPTION=y
```

* setup `fscrypt`:

```
sudo fscrypt setup
```

```
Defaulting to policy_version 2 because kernel supports it.
Customizing passphrase hashing difficulty for this system...
Created global config file at "/etc/fscrypt.conf".
Metadata directories created at "/.fscrypt".
```

* Verify: 

```
fscrypt status
filesystems supporting encryption: 1
filesystems with fscrypt metadata: 1

MOUNTPOINT  DEVICE          FILESYSTEM  ENCRYPTION     FSCRYPT
/           /dev/nvme0n1p3  ext4        supported      Yes
/boot       /dev/nvme0n1p2  ext4        not enabled    No
```

### PAM configuration

* Select the minimal profile with `authselect`

```
sudo authselect select minimal --force
```

* Activate the `ecryptfs` feature

```
sudo authselect enable-feature with-ecryptfs
```

* Create a new profile based on the minimal profile and call it phyllome:

``` 
sudo authselect create-profile phyllome --base-on=minimal 
``` 
```
New profile was created at /etc/authselect/custom/phyllome
```

* Select the newly create profile:

```
sudo authselect select custom/phyllome --force
```

```
Backup stored at /var/lib/authselect/backups/2021-07-15-20-08-13.4Czqor
Profile "custom/phyllome" was selected.
The following nsswitch maps are overwritten by the profile:
- aliases
- automount
- ethers
- group
- hosts
- initgroups
- netgroup
- networks
- passwd
- protocols
- publickey
- rpc
- services
- shadow
``` 

* Modify the content of the *system-auth* file:

```
sudo nano /etc/authselect/custom/phyllome/system-auth
```

```
auth        required                                     pam_env.so
auth        required                                     pam_faildelay.so delay=2000000
auth        required                                     pam_faillock.so preauth silent      >
auth        sufficient                                   pam_unix.so {if not "without-nullok">
auth        required                                     pam_faillock.so authfail            >
auth        required                                     pam_deny.so
auth        optional                                     pam_fscrypt.so

account     required                                     pam_access.so                       >
account     required                                     pam_faillock.so                     >
account     required                                     pam_unix.so

password    requisite                                    pam_pwquality.so
password    sufficient                                   pam_unix.so yescrypt shadow {if not >
password    required                                     pam_deny.so
password    optional                                     pam_fscrypt.so

session     optional                                     pam_keyinit.so revoke
session     required                                     pam_limits.so
session     optional                                     pam_fscrypt.so
-session    optional                                     pam_systemd.so
session     optional                                     pam_oddjob_mkhomedir.so             >
session     [success=1 default=ignore]                   pam_succeed_if.so service in crond q>
session     required                                     pam_unix.so
```

> *According to [fscrypt documentation](https://github.com/google/fscrypt#enabling-the-pam-module-on-other-linux-distros), *The Auth and Session functionality of `pam_fscrypt.so` are used to automatically unlock directories when logging in as a user, and lock them when logging out [and] [t]he Password functionality [...] is used to automatically rewrap a user's login protector when their unix passphrase changes."* *
{.is-info}

* Copy content of *system-auth* file into a the *password-auth* file.

> *Unsure which file is the canonic one*
{.is-info}

`sudo cp system-auth password-auth`

* Modify the *postlogin* file as well to match the following content

```
auth        optional                   pam_fscrypt.so debug  

password    optional                   pam_fscrypt.so debug  

session     optional                   pam_umask.so silent
session     [success=1 default=ignore] pam_succeed_if.so service !~ gdm* service !~ su* quiet
session     [default=1]                pam_lastlog.so nowtmp {if "with-silent-lastlog":silent>
session     optional                   pam_lastlog.so silent noupdate showfailed
``` 

* Create the fscrypt file under the `/etc/pam.d/` directory and add the following line to it to allow PAM to be able to check the UNIX passhphrase

```
nano /etc/pam.d/fscrypt
```

`auth        required    pam_unix.so`

* Finally, apply changes to phyllome profile

```
authselect apply-changes
Changes were successfully applied.
```

### Tame SELinux

> *This is a work in progress. New policices will have to be designed for SELinux to work nicely with fscrypt.
{.is-warning}

* Create a directory to store user-created SELinux policies and move there

```
sudo mkdir /opt/selinux && cd /opt/selinux/
```

* Allowing `systemd` to access 1000.count file
```
ausearch -c '(systemd)' --raw | audit2allow -M my-systemd
``` 
```
semodule -X 300 -i my-systemd.pp
```

### Test

* Create a directory called `secret` in your home directory 

```
mkdir ~/secret
```

* Encrypt the directory using your login passhprase

```
fscrypt encrypt ~/secret --source=pam_passphrase
```

```
IMPORTANT: Before continuing, ensure you have properly set up your system for
           login protectors.  See
           https://github.com/google/fscrypt#setting-up-for-login-protectors
Enter login passphrase for test: 
"/home/groot/secret" is now encrypted, unlocked, and ready for use.
``` 

* Add a file to this directory

```
touch ~/secret/recipe-for-pancakes-by-john-locke
```

* Reboot and make sure the file can be red after login

```
cat ~/secret/recipe-for-pancakes-by-john-locke
``` 

``` 
Pancakes
* Take sweet cream 3/4 + pint. 
* Flower a quarter of a pound. 
* Eggs 7 leave out of 4 of the whites. 
* Beat the Eggs very well. 
* Then put in the flower, beat it a quarter of an hower. 
* Then put in six spoonfulls of the Cream, beat it a litle Take new sweet butter half a pound. * Melt it to oyle, & take off the skum, power in all the clear by degrees beating it all the time. 
* Then put in the rest of your cream. beat it well. 
* Half a grated nutmeg & litle orangeflower water. Frie it without butter.
This is the right way
```

## Encrypt virtual disks

* Encrypt default directory containing virtual disks for the current user

```
fscrypt encrypt ~/.local/share/libvirt/images --source=pam_passphrase
```

> *`fscrypt` does **not** support in-place encryption. Only previously empty directories can be encrypted. If you wish to encrypt a directory which already contains files, move these files outside of the directory, encrypt it, and put the files back in* 
{.is-warning}

### Post-installation cleaning (untested)

```
# dnf remove -y git golang m4
$ rm -rf ~/go
```

## Resources

### Troubleshooting

* You can use the following command to check for entries related to fscrypt in your log

```
journalctl -b | grep fscrypt
```

* If directories encrypted with `fscrypt` won't unlock, you could try to set SELinux in permissive mode and check error messages using the `setroubleshoot` software:

```
sudo nano /etc/selinux/config
```

``` 
SELINUX=permissive
```

Then reboot.

### Paths

* Where authselect stores its default and vendor-specific configs:
```
/usr/share/authselect/
```

* Where PAM modules are stored:
```
/usr/lib64/security/
```

* Where authselect stores the current profile

```
/etc/authselect
```

* Documentation on developing PAM modules

```
/usr/share/doc/pam-devel
```

/usr/local/share/pam-configs/fscrypt

Created global config file at "/etc/fscrypt.conf".
Metadata directories created at "/.fscrypt".

### External Resources

*The `fscrypt` PAM module implements the Auth, Session, and Password
[types](http://www.linux-pam.org/Linux-PAM-html/sag-configuration-file.html).*

* [fscrypt official repo](https://github.com/google/fscrypt)
* [PAM and Fedora](https://docs.fedoraproject.org/en-US/Fedora/17/html/Security_Guide/sect-Security_Guide-Pluggable_Authenticati1542858)
* [fscrypt for ext4 encryption on the Archwiki](https://wiki.archlinux.org/title/Fscrypt)
* [See here for an RPM package for altlinux](https://altlinux.pkgs.org/sisyphus/classic-x86_64/fscrypt-0.3.0.0.5.e479779-alt1.x86_64.rpm.html)
 