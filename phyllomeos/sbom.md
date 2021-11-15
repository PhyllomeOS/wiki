---
title: Software bill of materials (SBOM)
description: 
published: true
date: 2021-11-13T17:45:59.804Z
tags: 
editor: markdown
dateCreated: 2021-11-12T15:32:04.404Z
---

> Section under construction.
{.is-warning}

# List of software

The basic idea is to list software Phyllome OS relies on to function. 

## Fedora Server core

**316** is the number of installed packages on a minimal Fedora server system, which is used as a base for Phyllome OS.

The following list is provided by the following command `dnf list --installed | wc -l | sort` on a fresh installation. A description has been added.

* acl
	* Access Control Lists
	* Website : https://en.wikipedia.org/wiki/Access-control_list
* alternatives
	* Maintains symbolic links determining default commands
* audit and audit-libs 
	* Allows to control the kernel audit system through the *auditctl* command
* basesystem
	* "*the basesystem package defines the components of a basic Fedora system, such as the package installation during bootstrapping*."
* bash 
	* The GNU Bourne-Again SHell (BASH)
* bash-completion
* bzip2, bunzip2, bzip2-libs
	* A block-sorting file compressor
* c-ares
	* A C library that performs DNS requests and name resolves 
* ca-certificates
* chrony 
	* "chrony is a versatile implementation of the Network Time Protocol (NTP)"
	* Website : https://chrony.tuxfamily.org/
* compat-readline5.x86_64       
* coreutils and coreutils-common
	* Set of core utilities
* cpio 
	* "GNU cpio copies files into or out of a cpio or tar archive, The archive can be another file on the disk, a * magnetic tape, or a pipe."
	* Website : http://www.gnu.org/software/cpio/manual/cpio.html
* cracklib and cracklib-dicts
	* Cracklib is a library for checking whether password is easily crackable or not
	*  The sudo package depends on it
	*  Website : https://github.com/cracklib/cracklib
* crypto-policies and crypto-policies-scripts 
	* Cryptographic policy management
  * Website : https://github.com/linux-system-roles/crypto_policies/
* cryptsetup and cryptsetup-libs 
	* cryptsetup manages plain dm-crypt and LUKS encrypted volumes
* curl 
	* curl is used in command lines or scripts to transfer data
  * Website : https://curl.se/download.html
* cyrus, cyrus-sasl-gssapi, cyrus-sasl-lib, cyrus-sasl-plain.x86_64
	*  website : https://www.cyrusimap.org/sasl/
	*  sudo depends on cyrus
* d-bus - "D-Bus is a message bus system, a simple way for applications to talk to one another"
  * website : https://www.freedesktop.org/wiki/Software/dbus/
  * systemd depends on dbus
  * dbus, dbus-broker, dbus-common and dbus-libs            
* dejavu-sans-fonts and dejavu-sans-mono-fonts
	* package for dejavu font
  * dejavu-sans-fonts.noarch
  * dejavu-sans-mono-fonts.noarch
* deltarpm : rpm package manager
  * website : https://rpm.org/
  * deltarpm.x86_64
*  device-mapper : "The device mapper is provided by the Linux kernel to map physical block devices onto virtual * block devices"
*  grub2-tools-minimal depends on device-mapper
* device-mapper.x86_64          
* device-mapper-event.x86_64    
* device-mapper-event-libs.x86_64
* device-mapper-libs.x86_64     
* device-mapper-persistent-data.x86_64
*  dhcp-client - the dhcp-client package provides the ISC DHCP client daemon and dhclient-script
*  website : https://www.isc.org/dhcp/
* dhcp-client.x86_64
* dhcp-common.noarch
*  diffutils - GNU Diffutils is a package of several programs related to finding differences between files.
*  website : https://www.gnu.org/software/diffutils/
* policycoreutils depends on diffutils
* diffutils.x86_64
* dnf - dnf is the new package manager for Fedora
	* website : https://rpm-software-management.github.io/
	* dnf.noarch
	* dnf-data.noarch
	* dnf-plugins-core.noarch         
*  dosfstools - "dosfstools consists of the programs mkfs.fat, fsck.fat and fatlabel to create, check and label file * systems of the FAT family."
*  website : https://github.com/dosfstools/dosfstools
* dosfstools.x86_64
*  dracut - dracut is a set of tools to automate the Linux boot process
*  website : https://dracut.wiki.kernel.org/index.php/Main_Page
* dracut.x86_64
* dracut-config-rescue.x86_64
* dracut-network.x86_64          
*  e2fsprogs - e2fsprogs is a set of utilities to interact with ext2, ext3 and ext4 file systems
*  website : http://e2fsprogs.sourceforge.net/
* e2fsprogs.x86_64
* e2fsprogs-libs.x86_64
* efi-filesystem.noarch         
* efibootmgr.x86_64             
* efivar-libs.x86_64            
* elfutils-debuginfod-client.x86_64    
* elfutils-default-yama-scope.noarch   
* elfutils-libelf.x86_64               
* elfutils-libs.x86_64   
*  expat - expat is an XML parser library
*  systemd depends on expat
* expat.x86_64
*  fedora-* - fedora signing gpg-key and packages linked to fedora repositories
* fedora-gpg-keys.noarch               
* fedora-release.noarch         
* fedora-release-common.noarch  
* fedora-release-identity-basic.x86_64  
* fedora-repos.noarch                  
* fedora-repos-modular.noarch
*  file — software that determines file type
* file.x86_64
* file-libs.x86_64
*  filesystem - filesystem provides the basic directory layout for a Linux system
* filesystem.x86_64
*  findutils - "The GNU Find Utilities are the basic directory searching utilities of the GNU operating system".
*  website : https://www.gnu.org/software/findutils/
*  dracut depends on it
* findutils.x86_64
*  firewalld : "Firewalld provides a dynamically managed firewall with support for network/firewall zones that define * the trust level of network connections or interfaces."
*  website : https://firewalld.org/
* firewalld.noarch                     
* firewalld-filesystem.noarch          
*  fonts-filesystem - provides directories used by font packages
* fonts-filesystem.noarch
*  fuse-libs - "Fuselibs is the Uno-libraries that provide the UI framework used in Fuse apps."
*  website : https://github.com/fuse-open/fuselibs
*  grubs2-tools-minimal depends on fuse-libs
* fuse-libs.x86_64
*  awk - awk search files for lines that contain certain patterns.
*  website : https://www.gnu.org/software/gawk/
*  sudo depends on gawk
* gawk.x86_64
*  gdbm-libs - GNU dbm (GDBD) is a library of database functions
*  website : https://www.gnu.org.ua/software/gdbm/
*  dnf depends of gdbm-libs
* gdbm-libs.x86_64
*  gettext - translate message
*  grub2-pc depends on it
* gettext.x86_64
* gettext-libs.x86_64
*  glib - "The GLib package contains low-level libraries useful for providing data structure handling for C, * portability wrappers and interfaces for such runtime functionality as an event loop, threads, dynamic loading and * an object system."
*  website (not the official website) : https://www.linuxfromscratch.org/blfs/view/svn/general/glib2.html
*  dnf, grub2-tools-minimal, sudo, systemd depend on glib
* glib-networking.x86_64
* glib2.x86_64
* glibc.x86_64
* glibc-common.x86_64
* glibc-doc.noarch
* glibc-langpack-en.x86_64
*  gmp - gmp provides multiple precision arithmetic using the C library
*  website : https://cran.r-project.org/web/packages/gmp/index.html
*  grub2-pc, dnf, systemd depend on gmp
* gmp.x86_64
*  gnupg2 - GnuPG is a free OpenPGP implementation
*  website : https://gnupg.org/
*  dnf, grub2-pc, systemd, dnf depend gnupg2
* gnupg2.x86_64
*  gnutls - "GnuTLS is a secure communications library"
*  website : https://gnutls.org/
* gnutls.x86_64
*  gobject-introspection - "GObject introspection is a middleware layer between C libraries (using GObject) and * language bindings"
*  website : https://gi.readthedocs.io/en/latest/
*  PackageKit depends on gobject-introspection
* gobject-introspection.x86_64
* f remove -y gobject-introspection
*  "GnuPG Made Easy (GPGME) is a library designed to make access to GnuPG easier for applications."
*  website : https://www.gnupg.org/software/gpgme/index.html
*  dnf depends on gpgme
* gpgme.x86_64
*  grep - "grep is a command-line utility for searching plain-text data sets"
*  website : https://en.wikipedia.org/wiki/Grep
* grep.x86_64
*  groff - "groff - front-end for the groff document formatting system"
*  website : (not official) https://linux.die.net/man/1/groff
*  man-db depends on it
* groff-base.x86_64
*  grub2 - bootloader
* grub2-common.noarch
* grub2-pc.x86_64
* grub2-pc-modules.noarch
* grub2-tools.x86_64
* grub2-tools-minimal.x86_64
*  grubby - command line tool for configuring grub, lilo, and elilo
*  website : (not official) https://linux.die.net/man/8/grubby
* grubby.x86_64                
*  gzip - gunzip, zcat - compress or expand files
* gzip.x86_64
*  hostname - show or set the system's host name
* hostname.x86_64
*  ima-evm-utils- "Integrity Measurement Architecture to know EXACTLY what has been run on your machine."
*  website : https://sourceforge.net/projects/linux-ima/
*  dnf depends on ima-evm-utils
* ima-evm-utils.x86_64
*  initscripts - initscripts are scripts to bring up network interfaces and legacy utilities in Fedora, using the * legacy System V system.
*  audit depends on initscripts
* initscripts.x86_64
* ipcalc.x86_64                        
*  ipset - "IP sets are a framework inside the Linux kernel, which can be administered by the ipset utility."
*  website : https://ipset.netfilter.org/
*  firewalld depends on ipset
* ipset.x86_64
* ipset-libs.x86_64
* iptables-legacy-libs.x86_64          
* iptables-libs.x86_64                 
* iptables-nft.x86_64  
*  iptables - "iptables is the userspace command line program used to configure the Linux 2.4.x and later packet * filtering ruleset."
*  website : https://www.netfilter.org/
*  firewalld and iptstate depend on iptables
* iptables-legacy-libs.x86_64          
* iptables-libs.x86_64
* iptables-nft.x86_64
*  iputils - iputils
*  dhcp-client depends on iputils
* iputils.x86_64
*  jansson - Jansson is a C library for dealing with JSON data
* jansson.x86_64
*  firewalld, mtr, teamd, nftables depends on it
*  json-c - "JSON-C implements a reference counting object model that allows you to easily construct JSON objects in * C"
*  website : http://json-c.github.io/json-c/
*  systemd depends on json-c
* json-c.x86_64
*  kdb - tools for managing Linux console, i.e. loading console fonts and keyboard maps.
*  website : http://kbd-project.org/
* kbd.x86_64
* kbd-misc.noarch
*  kernel - the allmighty Linux kernel
*  website : https://www.kernel.org/  
* kernel.x86_64                        
* kernel-core.x86_64                   
* kernel-modules.x86_64 
*  keyutils - in-kernel key management utilities, to accessing the kernel keyrings facility
*  cifs-utils and nfs-utils depend on keyutils
* keyutils.x86_64
* keyutils-libs.x86_64
*  kmod - kmod is a set of tools for managing Linux kernel modules
* kmod.x86_64
* kmod-libs.x86_64
*  kpartx - kpartx Create device maps from partition tables
* kpartx.x86_64
*  krb5 - kerberos library
*  website : https://web.mit.edu/kerberos/krb5-1.16/doc/index.html
*  sudo depends on krb5
* krb5-libs.x86_64
*  langpacks-en - provides support for English
* langpacks-core-en.noarch
* langpacks-core-font-en.noarch
* langpacks-en.noarch
*  less - less is a file pager, a tool that display a screen at a time
*  website : https://packages.debian.org/stretch/less
* less.x86_64
*  various libraries
* libacl.x86_64                 
* libaio.x86_64                 
* libarchive.x86_64             
* libargon2.x86_64              
* libassuan.x86_64              
* libattr.x86_64                
* libbasicobjects.x86_64        
* libblkid.x86_64               
* libbrotli.x86_64              
* libcap.x86_64                 
* libcap-ng.x86_64              
* libcbor.x86_64                
* libcollection.x86_64          
* libcom_err.x86_64             
* libcomps.x86_64                      
* libcurl.x86_64                       
* libdb.x86_64                  
* libdhash.x86_64               
* libdnf.x86_64                        
* libeconf.x86_64               
* libedit.x86_64                       
* libfdisk.x86_64               
* libffi.x86_64                 
* libfido2.x86_64               
* libgcc.x86_64                        
* libgcrypt.x86_64                     
* libgomp.x86_64                       
* libgpg-error.x86_64           
* libibverbs.x86_64                    
* libidn2.x86_64                       
* libini_config.x86_64          
* libkcapi.x86_64               
* libkcapi-hmaccalc.x86_64      
* libksba.x86_64                
* libldb.x86_64                        
* libmaxminddb.x86_64           
* libmetalink.x86_64            
* libmnl.x86_64                 
* libmodulemd.x86_64                   
* libmount.x86_64               
* libndp.x86_64                 
* libnetfilter_conntrack.x86_64 
* libnfnetlink.x86_64           
* libnfsidmap.x86_64                   
* libnftnl.x86_64               
* libnghttp2.x86_64             
* libnl3.x86_64                 
* libnsl2.x86_64                
* libpath_utils.x86_64          
* libpcap.x86_64                       
* libpipeline.x86_64            
* libpsl.x86_64                 
* libpwquality.x86_64           
* libref_array.x86_64           
* librepo.x86_64                       
* libreport-filesystem.noarch  
*  libseccomp - library associated to seccomp
* libseccomp.x86_64
*  libselinux - library associated to libselinux
* libselinux.x86_64
* libselinux-utils.x86_64
* libsemanage.x86_64            
* libsepol.x86_64               
* libsigsegv.x86_64             
* libsmartcols.x86_64           
* libsolv.x86_64    
* libss.x86_64                  
*  librairies used by ssh ?
* libssh.x86_64
* libssh-config.noarch
*  librairies used by sssd ?
* libsss_autofs.x86_64                 
* libsss_certmap.x86_64                
* libsss_idmap.x86_64                  
* libsss_nss_idmap.x86_64              
* libsss_sudo.x86_64                   
*  various libraries
* libstdc++.x86_64                     
* libtalloc.x86_64              
* libtasn1.x86_64               
* libtdb.x86_64                 
* libtevent.x86_64              
* libtextstyle.x86_64           
* libtirpc.x86_64                      
* libunistring.x86_64           
* liburing.x86_64               
* libusbx.x86_64                
* libuser.x86_64                       
* libutempter.x86_64            
* libuuid.x86_64                
* libverto.x86_64               
* libxcrypt.x86_64                     
* libxcrypt-compat.x86_64              
* libxkbcommon.x86_64                  
* libxml2.x86_64                       
* libyaml.x86_64                
* libzstd.x86_64                       
*  linux-firmware - Firmware files for Linux
* linux-firmware.noarch                
* linux-firmware-whence.noarch         
*  lmdb - database linked to openLDAP ?
* lmdb-libs.x86_64
*  lua-libs - "lua-libs is a collection of utilities, oop, linked list, memoization, memento, flyweight, string * manipulation"
*  website : (not official) http://lua-users.org/wiki/LibrariesAndBindings
* lua-libs.x86_64
*  LVM
* lvm2.x86_64                   
* lvm2-libs.x86_64   
*  lz4-libs - LZ4 is lossless compression algorithm
*  website : https://lz4.github.io/lz4/
*  systemd depends on lz4-libs
* lz4-libs.x86_64
*  man-pages - conventions for writing Linux man pages
* man-db.x86_64                 
* mkpasswd.x86_64    
* mokutil.x86_64    
*  mpfr - MPFR is based on the GMP multiple-precision library
*  website : https://www.mpfr.org/
* mpfr.x86_64
*  ncurses - "ncurses is a programming library providing an application programming interface that allows the * programmer to write text-based user interfaces in a terminal-independent manner." https://invisible-island.net/* ncurses/announce.html
* ncurses.x86_64
* ncurses-base.noarch
* ncurses-libs.x86_64   
*  nettle - Nettle is a cryptographic library that is designed to fit easily in more or less anycontext: In crypto * toolkits for object-oriented languages (C++, Python, Pike, ...), inapplications like LSH or GNUPG, or even in * kernel space.
*  website : https://www.lysator.liu.se/~nisse/nettle/
* nettle.x86_64
*  nftables - "nftables is the successor of iptables, it allows for much more flexible, scalable and performance * packet classification".
*  website : https://www.nftables.org/
* nftables.x86_64
*  nPth is a non-preemptive threads implementation
* npth.x86_64
*  openldap - the openLDAP directory
*  sudo depends on openldap
* openldap.x86_64
*  openssh
* openssh.x86_64                       
* openssh-clients.x86_64               
* openssh-server.x86_64  
*  openssl - a general purpose cryptography library with TLS implementation
* openssl-libs.x86_64  
*  os-prober - discover bootable partitions on the local system. See https://www.linux.org/docs/man1/os-prober.html
*  grub2-pc depends on os-proper
* os-prober.x86_64
*  p11-kit - "Provides a way to load and enumerate PKCS#11 modules"
*  website : https://p11-glue.github.io/p11-glue/p11-kit.html
*  systemd depends on p11-kit
* p11-kit.x86_64
* p11-kit-trust.x86_64
*  pam - Pluggable Authentication Modules (PAM) for Linux
*  website : http://www.linux-pam.org/
* pam.x86_64
* pam_passwdqc.x86_64
*  parted - parted manipulates partitions
*  website : http://www.gnu.org/software/parted/
* parted.x86_64
* f remove -y parted
*  passwd - update user's authentication tokens
* passwd.x86_64
* passwdqc.x86_64
* passwdqc-utils.x86_64
*  pcre - pcre (Perl Compatible Regular Expressions) provides regular expressions for Perl
*  website : http://www.pcre.org/
* pcre.x86_64
* pcre2.x86_64
* pcre2-syntax.noarch
*  plymouth - "Plymouth is an application that runs very early in the boot process (even before the root filesystem * is mounted!) that provides a graphical boot animation while the boot process happens in the background."
*  website : https://www.freedesktop.org/wiki/Software/Plymouth/
* plymouth.x86_64
* plymouth-core-libs.x86_64
* plymouth-scripts.x86_64    
*  policycoreutils - SELinux policy core utilities
*  website : http://www.selinuxproject.org/page/Main_Page
* policycoreutils.x86_64
*  popt - "The library popt parses options in command lines in Linux and other Unix-like systems."
*  website - https://github.com/devzero2000/POPT
* popt.x86_64
*  procps - "Command line and full screen utilities for browsing procfs, a "pseudo" file system dynamically generated * by the kernel to provide information about the status of entries in its process table."
* procps-ng.x86_64
*  psmisc - "A package of small utilities that use the proc file-system."
*  website : https://gitlab.com/psmisc/psmisc
* psmisc.x86_64
*  publicsuffix - "Cross-vendor public domain suffix database in DAFSA form"
*  website : https://publicsuffix.org/learn/
* publicsuffix-list-dafsa.noarch
*  python-related - to-do

* python-pip-wheel.noarch              
* python-setuptools-wheel.noarch       
* python-unversioned-command.noarch    
* python3.x86_64                       
* python3-dateutil.noarch       
* python3-dbus.x86_64           
* python3-decorator.noarch      
* python3-distro.noarch         
* python3-dnf.noarch                   
* python3-dnf-plugins-core.noarch      
* python3-firewall.noarch              
* python3-gobject-base.x86_64   
* python3-gpg.x86_64            
* python3-hawkey.x86_64                
* python3-libcomps.x86_64              
* python3-libdnf.x86_64                
* python3-libs.x86_64                  
* python3-libselinux.x86_64     
* python3-nftables.x86_64       
* python3-pip.noarch                   
* python3-rpm.x86_64            
* python3-setuptools.noarch            
* python3-six.noarch            
* python3-slip.noarch           
* python3-slip-dbus.noarch

*  qemu-guest-agent - "The QEMU Guest Agent is a daemon intended to be run within virtual machines"
*  website : https://qemu.readthedocs.io/en/latest/interop/qemu-ga-ref.html
* qemu-guest-agent.x86_64
*  readline - allows to edit command lines as they are typed in
*  website : https://tiswww.case.edu/php/chet/readline/rltop.html
*  systemd depends on readline
* readline.x86_64
*  rootfiles - the root file system
* rootfiles.noarch
*  rpm - "The RPM Package Manager (RPM) is a powerful package management system"
*  website : https://rpm.org/
* rpm.x86_64                    
* rpm-build-libs.x86_64         
* rpm-libs.x86_64               
* rpm-plugin-selinux.x86_64     
* rpm-sign-libs.x86_64          
* rpmfusion-free-release.noarch    
*  sed - sed (stream editor) is a non-interactive command-line text editor.
*  website : https://www.gnu.org/software/sed/
*  grub2-pc depends on sed
* sed.x86_64
*  selinux-policy - "The SELinux Policy is the set of rules that guide the SELinux security engine."
*  website : https://web.mit.edu/rhel-doc/5/RHEL-5-manual/Deployment_Guide-en-US/rhlcommon-chapter-0001.html
* selinux-policy.noarch
* selinux-policy-targeted.noarch
*  ???
* setup.noarch                 
*  shadow-utils - "Utilities for managing accounts and shadow password files"
*  website : https://yum-info.contradodigital.com/view-package/installed/shadow-utils/
* shadow-utils.x86_64
*  shared-mime-info - MIME database to represent types of files.
*  website - https://freedesktop.org/wiki/Specifications/shared-mime-info-spec/
*  PackageKit depends on shared-mime-info
* shared-mime-info.x86_64
*  ???
* shim-x64.x86_64               
*  sqlite-libs - C library that implements a SQL database engine
*  website - https://sqlite.org/index.html
*  dnf depends on sqlite-libs
* sqlite-libs.x86_64
*  sssd - the System Security Services Daemon (SSSD) allows Linux machines to enroll in AD, FreeIPA or LDAP
* sssd-client.x86_64                   
* sssd-common.x86_64                   
* sssd-kcm.x86_64                      
* sssd-nfs-idmap.x86_64      
*  sudo, sudoedit — sudo allows to execute a command as another user
* sudo.x86_64               
*  systemd - "systemd is a suite of basic building blocks for a Linux system".
*  website : https://systemd.io/
* systemd.x86_64                       
* systemd-libs.x86_64                  
* systemd-networkd.x86_64              
* systemd-oomd-defaults.x86_64         
* systemd-pam.x86_64                   
* systemd-rpm-macros.noarch            
* systemd-udev.x86_64            
*  tpm2-tss - "Trusted Computing Group's (TCG) TPM2 Software Stack (TSS)."
*  website : https://tpm2-tss.readthedocs.io/en/latest/index.html
* tpm2-tss.x86_64
*  tzdata - control and set timezones
* tzdata.noarch        
*  util-linux - "util-linux is a random collection of Linux utilities"
*  website : https://github.com/karelzak/util-linux
* util-linux.x86_64          
* vim-minimal - 
	* the vi editor
	* website : https://www.vim.org/
* vim-minimal.x86_64   
* which - shows the full path of (shell) commands.
	* grub2-pc depends on which
* whois-nls.noarch           
*  xkeyboard-config
*  website : https://github.com/freedesktop/xkeyboard-config
* xkeyboard-config.noarch
*  xz - "Compress or decompress .xz and .lzma files"
* xz.x86_64                     
* xz-libs.x86_64             
*  yum - yellowdog updater modified (yum) "is an automatic updater and package installer/remover for rpm systems"
*  website : http://yum.baseurl.org/
* yum.noarch                 
*  zchunk - compressed file format that provides easy deltas
* zchunk-libs.x86_64        
*  zlib
*  website : https://www.zlib.net/
* zlib.x86_64                   
*  zram - "zram-generator - Systemd unit generator for zram swap devices"
* zram-generator.x86_64         
* zram-generator-defaults.noarch