---
title: External ressources
description: A list of external mostly-online ressources around KVM virtualization and related technologies
published: true
date: 2021-06-23T13:20:50.700Z
tags: 
editor: markdown
dateCreated: 2021-06-23T12:36:12.051Z
---

# Curated ressources

## Meta 

* [Awesome Virtualization](https://github.com/Wenzel/awesome-virtualization), A curated list of awesome resources about virtualization

## Communities

* To-do

## Unsorted

* [Index of Documentation for People Interested in Writing and/or Understanding the Linux Kernel](http://www.dit.upm.es/~jmseyas/linux/kernel/hackers-docs.html)

## Books

### On Linux

* The Linux Command Line, 2nd Edition: A Complete Introduction
* Understanding the Linux Kernel 3e
* Linux System Programming 2ed
* The Linux Programming Interface: A Linux and UNIX System Programming Handbook (English Edition)

## Tools

### VMs management

* [Ignite from Weaveworks](https://github.com/weaveworks/ignite)

### Virt-* tools

* virt-install and cloud-init : https://blog.wikichoon.com/2020/09/virt-install-cloud-init.html
* virt-builder and virsh : https://developer.fedoraproject.org/tools/virt-builder/about.html
* virt-builder : https://www.admin-magazine.com/Articles/Generate-VM-Images-with-virt-builder
* https://docs.fedoraproject.org/en-US/fedora-silverblue/toolbox/
* https://www.golinuxcloud.com/virt-install-examples-kvm-virt-commands-linux/
* virt* cheatsheet : https://www.cyberithub.com/virsh-commands-examples-virt-df-virt-top-kvm/
* https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/sect-guest_virtual_machine_installation_overview-creating_guests_with_virt_install

### Kickstart

* https://docs.fedoraproject.org/en-US/fedora/rawhide/install-guide/advanced/Kickstart_Installations/
* https://fedoraproject.org/wiki/Anaconda/Kickstart/KickstartingFedoraLiveInstallation
* For reference, a complex example with CentOS : https://gist.github.com/giovtorres/0049cec554179d96e0a8329930a6d724

### Fedora-related 

* Redhat Fedora : https://developer.fedoraproject.org/tools.html
* Fedora Silverblue : https://docs.fedoraproject.org/en-US/fedora-silverblue/toolbox/

### Open Build Service (OBS)

* Our build tool, building all of our packages as well as ones for SUSE Linux Enterprise, Arch, Debian, Fedora, Scientific Linux, RHEL, CentOS, Ubuntu, and more : https://openbuildservice.org/

### openQA

* Automated testing for *any* operating system, that can read the screen and control the test host the same way a user does : http://open.qa/

### YaST

The best/only comprehensive Linux system configuration & installation tool : https://yast.opensuse.org/documentation

### Kiwi

Create Linux images for deployment on real hardware, virtualisation, and now even container systems like Docker. Kiwi is the engine that builds the openSUSE release images.

* http://osinside.github.io/kiwi/self_contained.html
* http://osinside.github.io/kiwi/building_images/build_live_iso.html
* http://osinside.github.io/kiwi/building_images/build_simple_disk.html
* http://osinside.github.io/kiwi/building_images/build_kis.html

## Virtual chipsets

### i440fx

### Q35

### microvm

### virt

## Devices 

### Emulated

### Paravirtualization

* [Virtual I/O Device (VIRTIO) specification, version 1.1](http://docs.oasis-open.org/virtio/virtio/v1.1/virtio-v1.1.html)

#### vfio-mdev

#### vfio-gpu

## KVM hypervisors

### CROSVM/KVM

#### Spectrum OS

* https://github.com/sponsors/alyssais
* https://liberapay.com/qyliss/
* https://spectrum-os.org/

### QEMU/KVM

* QEMU / KVM CPU model configuration : https://qemu.readthedocs.io/en/latest/system/qemu-cpu-models.html
* This is a port of QEMU machine emulator to JavaScript using Emscripten : https://github.com/atrosinenko/qemujs
* My QEMU fork with pinning (affinity) support and a few tweaks. : https://github.com/saveriomiroddi/qemu-pinning

#### QEMU virtualization on Fedora host

* [Virtualization Deployment and Administration Guide](https://docs.fedoraproject.org/en-US/Fedora_Draft_Documentation/0.1/html/Virtualization_Deployment_and_Administration_Guide/index.html) 
* https://docs.fedoraproject.org/en-US/Fedora/26/html/Installation_Guide/index.html
* fedora cloud images : https://alt.fedoraproject.org/cloud/

#### QEMU virtualization on macOS host

* Virtualizing OpenCore and x86 macOS on Apple Silicon (and even iOS!) https://khronokernel.github.io/apple/silicon/2021/01/17/QEMU-AS.html
* UTM App :
	* https://mac.getutm.app/
	* https://github.com/utmapp/UTM

### Cloud Hypervisor/KVM

* Docs ; https://github.com/cloud-hypervisor/cloud-hypervisor/tree/master/docs
* Cloud Hypervisor API : https://github.com/cloud-hypervisor/cloud-hypervisor/blob/master/docs/api.md
* Device model : https://github.com/cloud-hypervisor/cloud-hypervisor/blob/master/docs/device_model.md
* FUzzing : https://github.com/cloud-hypervisor/cloud-hypervisor/blob/master/docs/fuzzing.md
* Using MACVTAP to Bridge onto Host Network : https://github.com/cloud-hypervisor/cloud-hypervisor/blob/master/docs/macvtap-bridge.md
* Networking : https://github.com/cloud-hypervisor/cloud-hypervisor/blob/master/docs/networking.md
* UEFI Boot : https://github.com/cloud-hypervisor/cloud-hypervisor/blob/master/docs/uefi.md
* VFIO : https://github.com/cloud-hypervisor/cloud-hypervisor/blob/master/docs/vfio.md

## Guests

### Android

* adb cheat sheet : https://www.automatetheplanet.com/adb-cheat-sheet/
* Building Android for Qemu: A Step-by-Step Guide https://www.collabora.com/news-and-blog/blog/2016/09/02/building-android-for-qemu-a-step-by-step-guide/
* Vifio for Android : https://github.com/robherring/generic_device/wiki

### Lakka

* Proxmox : https://forums.libretro.com/t/video-guide-how-to-install-lakka-as-a-vm-using-kvm-in-unraid/6319

### macOS kvm guest

* https://github.com/kholia/OSX-KVM
* https://github.com/yoonsikp/macos-kvm-pci-passthrough
* https://github.com/foxlet/macOS-Simple-KVM
* https://www.nicksherlock.com/2019/10/installing-macos-catalina-10-15-on-proxmox-6/
* Virgil 3D renderer for macos : https://mail.gnu.org/archive/html/qemu-devel/2021-02/msg04235.html
* OSX-KVM : https://gitlab.com/sanselme/OSX-KVM

### PS4 

* Orbital : Virtualization-based PlayStation 4 emulator : https://github.com/AlexAltea/orbital

## Themes

### GPU-related

#### Android

* Android GPU Compute Going Forward  : https://android-developers.googleblog.com/2021/04/android-gpu-compute-going-forward.html?m=1
* GPU Emulation plans : https://groups.google.com/g/android-emulator-dev/c/9o8OZezxq9c?pli=1

#### Single GPU passthrough

* https://github.com/cosminmocan/vfio-single-amdgpu-passthrough
* https://gitlab.com/Karuri/vfio
* https://github.com/bducha/single-gpu-passthrough
* bugs : https://gitlab.freedesktop.org/mesa/mesa/-/issues/2678

## Guides

* Great in-depth article : https://stewartadam.io/howtos/fedora-20/create-gaming-virtual-machine-using-vfio-pci-passthrough-kvm
* UEFI ! https://blog.system76.com/post/139138591598/howto-uefi-qemu-guest-on-ubuntu-xenial-host
* Getting started with qemu : https://drewdevault.com/2018/09/10/Getting-started-with-qemu.html

## Package management

* RPM Packaging Guide : https://rpm-packaging-guide.github.io/#preparing-software-for-packaging
* Join the package collection maintainers : https://fedoraproject.org/wiki/Join_the_package_collection_maintainers

### Tiny-distro

*  Build and run minimal Linux / Busybox systems in Qemu : https://gist.github.com/chrisdone/02e165a0004be33734ac2334f215380e#file-gistfile1-md
*  Making minimal graphical operating system  : https://bcksp.blogspot.com/2017/09/making-minimal-graphical-operating.html?m=1
*  Build and boot a minimal Linux system with qemu : https://www.kaizou.org/2016/09/boot-minimal-linux-qemu.html
*  alux - a minimal Linux kernel distribution : https://github.com/alexhultman/alux
*  Build and run minimal linux with QEMU : https://gist.github.com/seokbeomKim/9cff93b073573fe535534c522c6e53e1

## Communication

### Mascot

* Xenia, the Linux mascot: https://xenia-linux-site.glitch.me/

## Funding

NGI Open Calls : https://www.ngi.eu/opencalls/#ngi-zero-pet-opencall

## MISC
* Isaard vdi : https://isard.gitlab.io/isardvdi-docs/#why-choose-isardvdi

## Desktop environment 

### Wayland

* GUI : http://bhepple.com/doku/doku.php?id=sway:sway-apps
* Wayland on archlinux : https://www.fosskers.ca/en/blog/wayland

## Virtualization tool

* https://docs.fedoraproject.org/en-US/Fedora/23/html/Virtualization_Getting_Started_Guide/sec-Other-Useful-tools.html
* https://github.com/kvmtool/kvmtool kvmtool is a lightweight tool for hosting KVM guests. As a pure virtualization tool it only supports guests using the same architecture, though it supports running 32-bit guests on those 64-bit architectures that allow this.

## Networking

### Bridge

* How To Create and Configure Bridge Networking For KVM in Linux : https://computingforgeeks.com/how-to-create-and-configure-bridge-networking-for-kvm-in-linux/
* https://docs.fedoraproject.org/en-US/Fedora/13/html/Virtualization_Guide/sect-Virtualization-Network_Configuration-Bridged_networking_with_libvirt.html
* Networking in Libvirt : https://wiki.libvirt.org/page/Networking
* https://lukas.zapletalovi.com/2015/09/fedora-22-libvirt-with-bridge.html
* How to Setup Bridge Networking with KVM on Ubuntu 20.04 : https://levelup.gitconnected.com/how-to-setup-bridge-networking-with-kvm-on-ubuntu-20-04-9c560b3e3991

### Bridge Wireless Cards

* https://shanetomlinson.com/bridging-a-wireless-card-in-kvmqemu/
* https://web.archive.org/web/20160821085327/http://blog.bodhizazen.net/linux/bridge-wireless-cards/
* https://gist.github.com/Jiab77/4cf278ac3ad59665969bdf73e083a847
* https://unix.stackexchange.com/questions/159191/setup-kvm-on-a-wireless-interface-on-a-laptop-machine


## Cloud gaming

* Gaming Anywhere : https://github.com/chunying/gaminganywhere

## Linux KVM

https://thereisnospoon.ews-network.net/posts/fedora-30-win10-nvidia-gpu-passthrough/
https://www.redhat.com/en/blog/all-you-need-know-about-kvm-userspace
Windows Gaming on Linux: Single GPU Passthrough Guide https://www.youtube.com/watch?v=3BxAaaRDEEw
Using the KVM API https://lwn.net/Articles/658511/
Sparkler: A KVM-based Virtual Machine Manager : https://unixism.net/2019/10/sparkler-kvm-based-virtual-machine-manager/

## 3D in a VM virtual gpu virtugl virtio-gl virgil

* Virglrenderer and the state of virtualized virtual worlds, 2019. https://www.collabora.com/news-and-blog/blog/2019/08/28/virglrenderer-state-of-virtualized-virtual-worlds/
* Virtualizing GPU Access https://www.collabora.com/news-and-blog/blog/2018/02/12/virtualizing-gpu-access/
* Android https://linuxhint.com/android_qemu_play_3d_games_linux/
* https://www.kraxel.org/blog/2016/09/using-virtio-gpu-with-libvirt-and-spice/
* https://src.fedoraproject.org/rpms/virglrenderer
* https://github.com/VirtualGL/virtualgl/releases
* https://virtualgl.org/About/Introduction
* http://virgil3d.github.io/
* https://www.studiopixl.com/2017-08-27/3d-acceleration-using-virtio.html
* https://cgit.freedesktop.org/virglrenderer
* https://github.com/Keenuts/virtio-gpu-documentation
* https://at.projects.genivi.org/wiki/display/DIRO/VIRTIO+GPU+Operation+Highlights
* https://www.reddit.com/r/archlinux/comments/7nmceg/kvmqemu_with_virtiogpu_virgl_support_enabled/
* https://forums.unraid.net/topic/62276-gpu-virtualization-virtio-gpu-virgl-sr-iov-mxgpu-vdi-spice/
* https://github.com/ekistece/Fedora-33-VFIO-guide/
* www.reddit.com/r/VFIO/comments/h9zijx/fedora_32_and_gpu_passthrough_vfio/
* https://czak.pl/2020/04/09/three-levels-of-qemu-graphics.html
* http://events17.linuxfoundation.org/sites/events/files/slides/KVM%20Forum%202014%20-%20VFIO%2C%20OVMF%2C%20GPU%2C%20and%20You%20-%20Alex%20Williamson.pdf
* Virgil 3d project homepage : http://virgil3d.github.io/
* Introducing Virgil - 3D virtual GPU for qemu : https://airlied.livejournal.com/77553.html

## Modes of 3D acceleration in a VM explained

https://www.kraxel.org/blog/2019/09/display-devices-in-qemu/

## Intel HAXM

 Nested virtualization support : https://github.com/intel/haxm/issues/51

# Gitea awesome list

Awesome Gitea : https://gitea.com/gitea/awesome-gitea

## Cloud-init

https://wiki.archlinux.org/title/Cloud-init

virt-install --cloud-init support : https://blog.wikichoon.com/2020/09/virt-install-cloud-init.html

## KVM server

[2016] Performant Security Hardening of KVM by Steve Rutherford : https://www.youtube.com/watch?v=vj5PA_D03Vg

Great guide : https://github.com/ekistece/Fedora-33-VFIO-guide/

https://mathiashueber.com/performance-tweaks-gaming-on-virtual-machines/

https://www.cyberciti.biz/faq/how-to-install-kvm-on-centos-8-headless-server/

https://ostechnix.com/install-and-configure-kvm-in-ubuntu-20-04-headless-server/

https://www.cyberciti.biz/faq/how-to-install-kvm-on-ubuntu-20-04-lts-headless-server/

https://computingforgeeks.com/how-to-install-kvm-on-fedora/

https://www.server-world.info/en/note?os=CentOS_7&p=kvm&f=10

'virt-host-validate' to check whether QEMU and LXC are setup correctly

https://scottlinux.com/2017/05/10/how-to-enable-iommu-support-in-fedora-linux/

https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF

https://heiko-sieger.info/creating-a-windows-10-vm-on-the-amd-ryzen-9-3900x-using-qemu-4-0-and-vga-passthrough/

https://marzukia.github.io/post/fedora-32-and-gpu-passthrough-vfio/

https://forum.level1techs.com/t/vfio-in-2019-fedora-workstation-general-guide-though-branch-draft/145106

https://marzukia.github.io/post/fedora-32-and-gpu-passthrough-vfio/

https://gitlab.com/Karuri/vfio

https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF

https://www.linux-kvm.org/page/KVM_Features

## Libvirt

https://wiki.archlinux.org/title/Libvirt

## Guest protection

https://www.computer.org/csdl/proceedings-article/hpca/2018/365901a441/12OmNzkMlRm

https://ipads.se.sjtu.edu.cn/_media/publications/fidelius_hpca18.pdf

## Nested virt. with KVM

https://www.rdoxenham.com/?p=275

https://docs.fedoraproject.org/en-US/quick-docs/using-nested-virtualization-in-kvm/


(Mostly) Exitless VM Protection from Untrusted Hypervisor through Disaggregated Nested Virtualization

https://www.usenix.org/conference/usenixsecurity20/presentation/mi

https://www.researchgate.net/publication/261020814_Architecture_support_for_guest-transparent_VM_protection_from_untrusted_hypervisor_and_physical_attacks


## Hackintosh

https://dortania.github.io/OpenCore-Install-Guide/installer-guide/linux-install.html#downloading-macos

## ACS Override

* Fedora ACS override https://github.com/Somersall-Natalie/fedora-acs-override
*  ACS Override Kernel Builds  https://queuecumber.gitlab.io/linux-acs-override/
*  Fedora Build ACS Override Patch Kernel https://wiki.myhypervisor.ca/books/linux/page/fedora-build-acs-override-patch-kernel
*  ACS Overrride patch for debian https://github.com/raphendyr/acs-override
*  [PATCH] pci: Enable overrides for missing ACS capabilities PCIe ACS (Access Control Services) : https://lkml.org/lkml/2013/5/30/513
*   IOMMU Groups, inside and out  http://vfio.blogspot.com/2014/08/iommu-groups-inside-and-out.html

## Security

### Secure Boot

https://www.kraxel.org/slides/virtual-secure-boot/#hands-on-libvirt

* [Openstack] Allow Secure Boot (SB) for QEMU- and KVM-based guests :
https://specs.openstack.org/openstack/nova-specs/specs/train/approved/allow-secure-boot-for-qemu-kvm-guests.html

### sVirt

http://www.virtualopensystems.com/en/solutions/guides/kvm-svirt-omap5/
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security-enhanced_linux/ch07s02
sVirt: Hardening Linux Virtualization with Mandatory Access Control https://www.youtube.com/watch?v=1e1gHOBduuQ

### Qemu

https://qemu.readthedocs.io/en/latest/system/security.html

### TPM
https://fossies.org/linux/qemu/docs/specs/tpm.rst

### Ideas from hackernews blog post (as used by Red Hat)

* Aggressively compile out unused features/devices.

* Confine each VM with separate SELinux contexts (sVirt).

* Run qemu as a special non-root user.

* Use seccomp to confine the system calls.

* Pass in pre-opened file descriptors to qemu, so qemu doesn't need to open files (helps with writing tightly confined SELinux policy).

* Run qemu in a cgroup.

* Run qemu-img with resource limits.

* Compile qemu with all hardening features enabled like RELRO, PIE, etc.

* Audit the code manually and with Coverity.

* Take security reports seriously and have a fast patching mechanism (you can effectively "live patch" qemu by migrating a VM off the old qemu and on to the new qemu).

Probably more that I've forgotten about ...

https://news.ycombinator.com/item?id=18588899

### Other ressources

ERNW_Hardening_KVM : https://github.com/ernw/hardening/blob/master/hypervisor/kvm/ERNW_Hardening_KVM.md

Security in QEMUHow Virtual Machines provide Isolation : https://vmsplice.net/~stefan/stefanha-kvm-forum-2018.pdf

Qemu hardening with CT: https://www.redhat.com/en/blog/hardening-qemu-through-continuous-security-testing


## Headless virtualization

https://www.ostechnix.com/setup-headless-virtualization-server-using-kvm-ubuntu/

https://www.cyberciti.biz/faq/installing-kvm-on-ubuntu-16-04-lts-server/

fedora headless virt group

## RESSOURCES Unraid

https://forums.unraid.net/topic/54834-video-guideall-about-docker-in-unraid-docker-principles-and-setup/

https://forums.unraid.net/topic/84226-wireguard-quickstart/

https://forums.unraid.net/topic/80251-unraid-beginners-tutorial/

https://forums.unraid.net/topic/84316-wireguard-vpn-tunneled-access/

https://forums.unraid.net/topic/84226-wireguard-quickstart/

https://vfio.blogspot.com/2014/08/iommu-groups-inside-and-out.html ACS Override

https://forums.unraid.net/topic/51230-video-guidehow-to-pass-through-an-nvidia-gpu-as-primary-or-only-gpu-in-unraid/ gpu primary

Add that line to network boot loader
  <boot order='2'/>

##  windows guest tweaking :

https://wiki.unraid.net/UnRAID_6/VM_Guest_Support

Additionally, in case you are using QEMU 4.0 (or higher) in combination with a Q35 chip, the flag ‘ioapic driver='kvm'‘ needs to be added in the features section (see excerpt marked blue).
https://mathiashueber.com/fighting-error-43-nvidia-gpu-virtual-machine/

## Q35 Versus i440fx

https://www.reddit.com/r/VFIO/comments/5ireij/differencesbenefits_between_i440fx_and_q35/
https://wiki.qemu.org/Features/Q35

## Storage-related file

### TRIM in VM

https://chrisirwin.ca/posts/discard-with-kvm/

### Drive options

https://heiko-sieger.info/qemu-system-x86_64-drive-options/

### Virtio-FS

https://www.tauceti.blog/post/qemu-kvm-share-host-directory-with-vm-with-virtio/

### RAW versus QCOW2

https://www.tutos.snatch-crash.fr/proxmox-raw-vs-qcow2-vs-vmdk/

### QCOW Encryption

https://github.com/qemu/qemu/commit/12f7efd02ee4e7144b842a1437defb997b9ae66b

https://libvirt.org/formatstorageencryption.html

https://patchwork.kernel.org/project/qemu-devel/patch/20170210170910.8867-14-berrange@redhat.com/

https://patchwork.kernel.org/project/qemu-devel/patch/20170126101827.22378-13-berrange@redhat.com/

https://www.berrange.com/posts/2015/03/17/qemu-qcow2-built-in-encryption-just-say-no-deprecated-now-to-be-deleted-soon/

### SeaBIOS versus edk2

https://mail.coreboot.org/pipermail/seabios/2014-February/007689.html

### Snapshot of efi-based VM

https://lists.gnu.org/archive/html/qemu-devel/2020-09/msg05221.html

https://bugzilla.redhat.com/show_bug.cgi?id=1881850

## IOMMU Exploit

* Thunderclap : https://www.ndss-symposium.org/wp-content/uploads/ndss2019_05A-1_Markettos_slides.pdf

## XML
* http://functionx.com/xml/Lesson04.htm

## Intel GVT-g

* https://wiki.gentoo.org/wiki/User:Shunlir/Intel_GVT-g
* https://libvirt.org/drvnodedev.html
* https://blog.tmm.cx/2020/05/15/passing-an-intel-gpu-to-a-linux-kvm-virtual-machine/
* https://blog.bepbep.co/posts/gvt/
* https://reposhub.com/cpp/miscellaneous/DualCoder-vgpu_unlock.html
* https://lantian.pub/en/article/modify-computer/laptop-intel-nvidia-optimus-passthrough.lantian/
* https://wiki.archlinux.org/title/Intel_GVT-g

