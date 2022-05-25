
---
layout: post
date: 2022-04-22 02:00:00 +0900
title: "Ubuntu 22.04 LTS Jammy Jellyfish Release Notes"
tags:
 - release-notes
authors:
    - name: Ubuntu Korean Translators
      bio: .
      email: ubuntu-l10n-ko@lists.ubuntu.com
      launchpad: ubuntu-l10n-ko
      github: ubuntu-kr
      profile: https://launchpad.net/@@/team-logo
---
# Jammy Jellyfish 릴리즈 노트

# 서문

이 **우분투 22.04 LTS** (Jammy Jellyfish)에 대한 릴리즈 노트에서는 해당 릴리즈에 대한 개요와 우분투와 flavour에서의 알려진 문제들의 문서를 제공합니다.

## 지원 기간

우분투 데스크톱, 우분투 서버, 우분투 Cloud, 우분투 Core의 유지보수 업데이트는 [2027 4월](https://wiki.ubuntu.com/Releases)까지 5년 동안 제공되고, 나머지 모든 flavour에 대해서는 3년간 지원됩니다. 추가적 보안 업데이트는 [ESM (Extended Security Maintenance).](https://ubuntu.com/security/esm)를 통해 지원됩니다.

# Ubuntu 22.04 LTS 받기

## Ubuntu 22.04 다운로드

가까운 지역에서 이미지를 다운로드 할 수 있습니다.

ISO나 플래시 가능한 이미지 다운로드:

  * [64 비트 x86 (AMD64) 우분투 데스크톱 및 서버](http://releases.ubuntu.com/22.04/)
  * [종종 다운로드 되는 우분투 이미지](http://cdimage.ubuntu.com/ubuntu/releases/22.04/release/)
  * [우분투 Cloud 이미지](http://cloud-images.ubuntu.com/daily/server/jammy/current/)
  * [Lubuntu](http://cdimage.ubuntu.com/lubuntu/releases/22.04/release/)
  * [Kubuntu](http://cdimage.ubuntu.com/kubuntu/releases/22.04/release/)
  * [우분투 Budgie](http://cdimage.ubuntu.com/ubuntu-budgie/releases/22.04/release/)
  * [우분투 Kylin](http://cdimage.ubuntu.com/ubuntukylin/releases/22.04/release/)
  * [우분투 MATE](http://cdimage.ubuntu.com/ubuntu-mate/releases/22.04/release/)
  * [우분투 Studio](http://cdimage.ubuntu.com/ubuntustudio/releases/22.04/release/)
  * [Xubuntu](http://cdimage.ubuntu.com/xubuntu/releases/22.04/release/)

# Ubuntu 21.10에서 업그레이드

**현재 22.04 LTS로의 업그레이드는 활성화 되어 있지 않지만 (snap, update-notifier의 버그로 인함) 수일 이내에 활성화 될 예정입니다.**

데스크톱 시스템에서 업그레이드 하려면:

  * 시스템 설정에서 "소프트웨어 & 업데이트"를 여십시오.
  * 세번째 탭인 "업데이트" 탭을 선택하시오.
  * "새 우분투 버전 알려주기" 드롭다운 메뉴를 "모든 새 버전"으로 바꾸십시오.
  * <kbd>Alt</kbd>+ <kbd>F2</kbd> 키를 누르고 명령 실행에 `update-manager -c`를 입력하십시오.
    * 업데이트 관리자가 열리고 다음과 같이 말할 겁니다: **새 버전의 우분투를 사용할 수 있습니다. 업그레이드 하시겠습니까?"**
  * 만약 되지 않으면 `/usr/lib/ubuntu-release-upgrader/check-new-release-gtk`로도 할 수 있습니다.
  * 업그레이드를 클릭하고 화면의 지시를 따르십시오. 

서버 시스템에서 업그레이드 하려면:

  * `/etc/update-manager/release-upgrades`에서 `Prompt`에 해당하는 줄이 normal으로 설정 되어있는지 확인 하십시오.
  * 업그레이드 도구를 `sudo do-release-upgrade` 명령어로 실행하시오.
  * 화면의 지시를 따르십시오. 

서버 업그레이드에서는 GNU Screen을 사용하고 연결이 끊겼을 때 자동적으로 다시 콘솔에 붙게 된다는 점에 유의 바랍니다.

우분투 데스크톱 및 우분투 서버의 오프라인 업그레이드 선택지는 없습니다. 공식 미러, 혹은 로컬에서 접근 가능한 미러와 연결 가능한지 미리 확인하고 위의 지시들을 따르길 바랍니다.

# New features in 22.04 LTS

## Updated Packages

## Linux kernel :penguin:

Ubuntu 22.04 LTS ships multiple optimized kernels on per-product basis:

* Ubuntu Desktop will automatically opt-into [v5.17](https://kernelnewbies.org/Linux_5.17) kernel on the latest generations of certified devices (`linux-oem-22.04`)
* Ubuntu Desktop uses a rolling HWE kernel (`linux-hwe-22.04`) on all other generations of hardware. The rolling HWE kernel is based on the [v5.15](https://kernelnewbies.org/Linux_5.15) kernel for 22.04.0 and 22.04.1 point releases
* Ubuntu Server defaults to a non-rolling LTS kernel v5.15 (`linux-generic`)
* Ubuntu Cloud and Devices use optimized kernels in collaboration with partners (v5.15+ with additional backports and features)

Additional optimized and certified kernel flavours will become available in Ubuntu 22.04 LTS in due course.

### NVIDIA drivers

Ubuntu 22.04 LTS adds linux-restricted-modules of NVIDIA drivers on ARM64, in addition to the existing x86_64. Users on ARM64 can now use `ubuntu-drivers` tool to install and configure NVIDIA drivers from the Ubuntu Archive.

### UDP disabled for NFS mounts
Since Ubuntu 20.10 ("Groovy Gorilla"), the kernel option `CONFIG_NFS_DISABLE_UDP_SUPPORT=y` is set and this disables using UDP as the transport for NFS mounts, regardless of NFS version.

In practice, if you try to use `udp`, you will get this error:
```
$ sudo mount f1:/storage /mnt -o udp
mount.nfs: an incorrect mount option was specified
```


## Toolchain Upgrades :hammer_and_wrench:

GCC was updated to the 11.2.0 release, binutils to 2.38, and glibc to 2.35. Python :snake: now ships at version 3.10.4, Perl :camel: at version 5.34.0. LLVM now defaults to version 14. golang defaults to version 1.18.x. rustc defaults to version 1.58.

In addition to OpenJDK 11, OpenJDK 18 is now provided (but not used for package builds).

Ruby :gem: was updated from v2.7.4 to v3.0.

## systemd v249.11
The init system was updated to systemd v249, using a solid .11 patchlevel for the LTS. Please refer to the upstream [changelog](https://github.com/systemd/systemd/releases/tag/v249) for more information about the individual features. We've enabled the userspace OOMD service and are shipping the `systemd-oomd` package by default on the "Ubuntu Desktop" flavour, to avoid overloaded systems and the need of the kernel's OOM killer to kick in. The OOMD status can be checked using `oomctl`.

## OpenSSL 3.0

We've upgraded the OpenSSL library to the new 3.0 version, which disables a lot of legacy algorithms by default, as detailed in their [migration guide](https://www.openssl.org/docs/manmaster/man7/migration_guide.html). In particular, certificates using SHA1 or MD5 as hash algorithms are now invalid under the default security level.

In addition to the upstream deprecations, please note that since Ubuntu 20.04 (Focal Fossa), the security level 2 (which is the default) disables the (D)TLS protocols below 1.2 (included).

Since the new version has an API bump, third-party packages that depend on libssl1.1 will need to be rebuilt to instead depend on libssl3, as the older ABI isn't provided anymore.

## Security Improvements :lock:

nftables is now the default backend for the firewall. All applications on the system must agree on whether they will use the legacy `xtables` backend or the newer `nftables` backend. [Bug 1968608](https://bugs.launchpad.net/bugs/1968608) provides some context that may be helpful. [Docker may not be ready for the new `nftables` backend](https://github.com/docker-snap/docker-snap/issues/68).

`ssh-rsa` is now [disabled by default in OpenSSH](https://www.openssh.com/txt/release-8.8). See [bug 1961833](https://bugs.launchpad.net/ubuntu/+source/openssh/+bug/1961833) to learn how to selectively re-enable it if necessary.  If you are upgrading a system remotely over SSH, you should check that you are not relying on this to ensure that you will retain access after the upgrade. 

`scp` offers a [`-s` command line option](http://manpages.ubuntu.com/manpages/jammy/en/man1/scp.1.html) to use [sftp mode rather than scp mode](https://www.openssh.com/txt/release-8.9) when handling remote filenames. This new, safer, behaviour will eventually become the default.

## Ubuntu Desktop

* Ubuntu now offers [10 color choices](https://discourse.ubuntu.com/t/yaru-accent-colors-are-coming-to-jammy/27200) each in dark and light styles
* Firefox is now only provided in Ubuntu as a snap. Some benefits include
  * Directly maintained by Mozilla
  * More maintainable for the entire Ubuntu LTS lifecycle
  * … Which means faster access to the newest Firefox versions
  * Easily switch to a different Firefox flavor with snap channels including `esr/stable`, `latest/candidate`, `latest/beta`, and `latest/edge`
  * Sandboxed for improved security hardening for this critical app
* Desktop icons are shown in the bottom right by default but this can be changed through new settings added to the Appearance panel of the Settings app.
* Also there are new settings to control the Dock look and behavior
* Dock devices and filemanager integration has been improved

### GNOME :footprints:

* GNOME has been updated to include new features and fixes from [GNOME 41](https://release.gnome.org/41/) and [GNOME 42](https://release.gnome.org/42/) 
* Several apps are still at their 41 version numbers to provide a more time-tested experience for the LTS desktop by mostly avoiding libadwaita.
* The new cross-desktop [dark style](https://discourse.ubuntu.com/t/ubuntu-22-04-lts-dark-style-changes/27206) preference is supported.
* GNOME Shell and mutter have lots of performance improvements including the triple buffering patch.
* The default session for most systems that don't have an Nvidia graphics card is now Wayland. If you need a non-Wayland session, you can choose the *Ubuntu on Xorg* session by clicking the gear button after selecting your name on the login screen.
* Hardware with privacy screen support is now supported
* RDP is now available for sharing your desktop remotely. Legacy VNC is still available, but it is strongly recommended to use RDP for better security, privacy, and performance. If you were previously using VNC, you'll need to manually re-enable desktop sharing in the Settings app and get your new login information.

### Updated Applications

* Firefox 99 :fire::fox_face:
* [LibreOffice 7.3](https://wiki.documentfoundation.org/ReleaseNotes/7.3) :books:
* Thunderbird 91 :cloud_with_lightning::bird:

### Updated Subsystems

* [BlueZ 5.63](https://git.kernel.org/pub/scm/bluetooth/bluez.git/tree/ChangeLog?id=5.63)
* [CUPS 2.4](https://github.com/OpenPrinting/cups/blob/v2.4.1/CHANGES.md)
* [NetworkManager 1.36](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/-/blob/nm-1-36/NEWS)
* [Mesa 22](https://docs.mesa3d.org/relnotes/22.0.0.html)
* [Poppler 22.02](https://gitlab.freedesktop.org/poppler/poppler/-/blob/poppler-22.02.0/NEWS)
* [PulseAudio 16](https://www.freedesktop.org/wiki/Software/PulseAudio/Notes/16.0/)
* [xdg-desktop-portal 1.14](https://github.com/flatpak/xdg-desktop-portal/blob/1.14.2/NEWS)

## Ubuntu Server

#### Ubuntu HA/Clustering

##### Corosync

It was updated to version 3.16 which includes some new features:

* Support for changing crypto configuration during runtime. This includes turning cryptography on or off, changing *crypto_cipher* and *crypto_hash* and also changing of crypto key.
* Default token timeout was changed from 1 seconds to 3 seconds.
* Run *corosync -v* to get the list of supported crypto and compression models which can be used in corosync.conf
* Cgroup v2 support.

For the complete list of changes please refer to the [upstream release notes](https://github.com/corosync/corosync/releases).

##### Pacemaker

It was updated to version 2.1.2 which includes some new features:

* Add a new feature *priority-fencing-delay*. Optionally derive the priority of a node from the resource-priorities of the resources it is running.
* Add *on-fail=demot*e and *no-quorum-policy=demote* recovery policies for promoted resources.
* support for OCF Resource Agent API 1.1 standard.
* Many improvements in *crm_mon* and *crm_resource*.

For the complete list of changes please refer to the [upstream release notes](https://github.com/ClusterLabs/pacemaker/releases).

A notable difference from the version in Ubuntu Focal 20.04 is that the default configuration file does not define the node name as node1 anymore, now the output of uname -n is used as the default node name.

##### Resource agents

It was updated to version 4.7.0. Check the list of changes since Ubuntu Focal 20.04 [here](https://github.com/ClusterLabs/resource-agents/blob/main/ChangeLog#L95-L219).

The agents are now separated in two packages: resource-agents-base and resource-agents-extra. The resource-agents-base package contains the agents which are curated by the Ubuntu Server team, which means that automated tests are running in a continuous integration system to guarantee the quality of those agents. The resource-agents package is now a metapackage which depends on both resource-agents-base and resource-agents-extra. Please note that the resource-agents package will be removed in future releases; we recommend that you do not rely on its existence.

##### Fence agents

It was updated to version 4.7.1.

The agents are now separated in two packages: fence-agents-base and fence-agents-extra. The fence-agents-base package contains the agents which are curated by the Ubuntu Server team, which means that automated tests are running in a continuous integration system to guarantee the quality of those agents. The fence-agents package is now a metapackage which depends on both fence-agents-base and fence-agents-extra. Please note that fence-agents will be removed in releases; we recommend that you do not rely on its existence.

#### Containers runtime

##### containerd

It was updated to version 1.5.9. Some interesting changes are:

* Update pull to handle of non-https urls in descriptors
* Install apparmor parser for arm64 and update seccomp to 2.5.1
* Add support for *clone3* syscall to fix issue with certain images when seccomp is enabled
* Add image config labels in CRI container creation

For the complete list of changes please refer to the [upstream release page](https://github.com/containerd/containerd/releases).

##### runc

It was updated to version 1.1.0. There are many improvements and bug fixes which can be found in the [upstream release page](https://github.com/opencontainers/runc/releases). Some deprecations and removals which might impact the upgrade are presented below:

Deprecation

* runc run/start now warns if a new container cgroup is non-empty or frozen; this warning will become an error in runc 1.2

Removals

* cgroup.GetHugePageSizes has been removed entirely, and been replaced with cgroup.HugePageSizes which is more efficient
* intelrdt.GetIntelRdtPath has been removed. Users who were using this function to get the intelrdt root should use the new intelrdt.Root instead.

#### Ruby 3.0

The default Ruby interpreter was updated to version 3.0, whose goal is performance, concurrency, and Typing. To have a broad overview about the cool features and improvements check out the [Ruby 3.0 Release Announcement](https://www.ruby-lang.org/en/news/2020/12/25/ruby-3-0-0-released/).

Users coming from previous Ubuntu releases ( Ubuntu Focal 20.04 onward) will be moving from Ruby 2.7 to 3.0. In this case the [Ruby 2.7 Release Announcement](https://www.ruby-lang.org/en/news/2019/12/25/ruby-2-7-0-released/) might be useful as well. An important thing to keep in mind is that the following libraries are not bundled anymore in Ruby:

* sdbm
* webrick
* net-telnet
* xmlrpc

If you need these libraries, please install them separately.

Please pay attention to the Other Notable Changes since 2.7 section in the Ruby 3.0 Release announcement when migrating your application to Ruby 3.0.

#### PHP now defaults to version 8.1.2

PHP 8.1 contains many new features:  Enumerations allow defining custom types limited to a specific set of possible values, like using consts but with better type checking. Readonly properties prevent their value to be changed after initialization.  With first-class callable syntax, static analysis is easier to perform on PHP code, and allows creating anonymous functions such as Closures.  Intersection types allow specifying function parameters that must satisfy multiple type constraints; much like a union type expresses an A|B type relationship, intersection types allow expressing A&B types.  Many other new features, such as fibers, final class constraints, never return values, explicit octal numeral notation, use of new inside initializers, and more will allow writing tighter, more expressive PHP code.

PHP 8.1 also received significant attention to performance, with a 23% speedup for the Symfony Demo test, and a 3.5% speedup for WordPress, as compared with PHP 8.0.  A few of the performance-related features included in PHP 8.1 include an inheritance cache, fast class name resolution, and various optimizations to timelib, ext/date, SPL file-system interators, serialize/unserialize, and several heavily used internal functions.

Users of PHP 7.4 should note that version 8 removes a [number of deprecated functionalities](https://wiki.php.net/rfc/deprecations_php_7_4) and when upgrading should be prepared to make the appropriate changes to their applications.

#### OpenLDAP 2.5.x series

If you are updating from Ubuntu Focal 20.04, you will encounter a new major OpenLDAP release on Ubuntu Jammy 22.04: version 2.5.11.  This release brings several changes, new features and deprecations/removals. A non-exhaustive list of things to be aware of during the upgrade process is:

* The shell (`slapd-shell`), the BDB and the HDB backends have all been removed.
* The `ppolicy` module now provides its own built-in schema. The external `ppolicy` schema has been removed.
* The `nssov` module has been removed.

In certain situations, it is possible that the post-installation scripts will **not** be able to successfully migrate your current installation to new formats (e.g., when you are using an old backend like BDB/HDB). If this happens, you will be notified about the failure and the `slapd` server will **not** be (re)started; you will then have to take manual action in order to migrate your data and start the service. Please look at the [README.Debian ](https://git.launchpad.net/ubuntu/+source/openldap/tree/debian/slapd.README.Debian?h=ubuntu/impish-devel) file (under `/usr/share/doc/slapd/`) for more information.

#### BIND 9.18

BIND 9 has been updated to [version 9.18.1](https://bind9.readthedocs.io/en/v9_18_1/notes.html). This new version includes

- Support for DNS over TLS (DoT) and DNS over HTTPS (DoH).
- `named` now supports zone transfers over TLS (XFR-over-TLS, XoT) for both incoming and outgoing zone transfers.
- `dig` is now able to send DoT queries.

Users upgrading from previous versions should be aware of the following changes:

- The binary files which are neither daemons nor administrative programs have been moved from `/usr/sbin` to `/usr/bin`.
- Support for the map zone file format has been removed. Users relying on such zone file format should convert their zones to use the raw format and change configurations accordingly before upgrading.
- Several obsolete, non-working configuration options have been removed and are now treated as configuration failures when present. A complete list of such configurations is available in the [upstream release notes](https://bind9.readthedocs.io/en/v9_18_1/notes.html#removed-features).

#### Apache has been updated to 2.4.52 from 2.4.48.

 - OpenSSL support is improved to support OpenSSL v3.  mod_ssl also received various refinements for outgoing connection behaviors, backwards compatibility, and wireshark logging.
 - mod_md adds support for ACME External Account Binding (EAB) along with a host of other enhancements and fixes.
 - Numerous fixes, including better hostname and UDS URI checking and handling, status code responses, and so on.


#### PostgreSQL 14

PostgreSQL has been updated to version 14.2.

This update contains many new features and enhancements, including:

- Stored procedures can now return data via OUT parameters.
- The SQL-standard SEARCH and CYCLE options for common table expressions have been implemented.
- Subscripting can now be applied to any data type for which it is a useful notation, not only arrays. In this release, the jsonb and hstore types have gained subscripting operators.
- Range types have been extended by adding multiranges, allowing representation of noncontiguous data ranges.
- Numerous performance improvements have been made for parallel queries, heavily-concurrent workloads, partitioned tables, logical replication, and vacuuming.
- B-tree index updates are managed more efficiently, reducing index bloat.
- VACUUM automatically becomes more aggressive, and skips inessential cleanup, if the database starts to approach a transaction ID wraparound condition.
- Extended statistics can now be collected on expressions, allowing better planning results for complex queries.
- libpq now has the ability to pipeline multiple queries, which can boost throughput over high-latency connections.

These and a long list of further enhancements as well as bug fixes can be found in the release notes of [v14](https://www.postgresql.org/docs/14/release-14.html), [v14.1](https://www.postgresql.org/docs/release/14.1/), and [v14.2](https://www.postgresql.org/docs/release/14.2/).

#### Django 3.2.12

Django was updated from the previous LTS version 2.2 to the new LTS version 3.2.

The update contains many new features and bug fixes such as:

- Automatic AppConfig discovery
- Type customization of auto-created primary keys
- Functional indexes
- Asynchronous views and middleware support
- JSONField for all supported database backends
- And various further major and minor features, see the see the [release notes](https://docs.djangoproject.com/en/4.0/releases/3.2/) for more

Users upgrading from previous versions should be aware of the following backwards incompatibilities:

Changes have been made to:
- The Database backend API
- django.contrib.admin
- AbstractUser.first_name max_length - changed to 150
- Model.save() when providing a default for the primary key
- Along with various minor module changes 

For additional information, especially since an upgrade would be from the former v2.2 LTS to v3.2 LTS do not only check the Django project release notes of [3.2](https://docs.djangoproject.com/en/4.0/releases/3.2/) but also [3.1](https://docs.djangoproject.com/en/4.0/releases/3.1) and [3.0](https://docs.djangoproject.com/en/4.0/releases/3.0) as well as the various minor releases included up to 3.2.12 that is in Ubuntu 22.04.

#### MySQL 8.0

MySQL has been updated to version 8.0.28 in Jammy Jellyfish alongside Focal Fossa and Impish Indri.
It contains new features such as:

- The audit_log_disable system
- Data type updates
- The CPU_TIME statement metric

See the [8.0.28 upstream release notes](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-28.html) for more information.


#### NFS server
The NFS server and client packages have finally been updated to the latest upstream version.

All NFS services now read their configuration from `/etc/nfs.conf` and `/etc/nfs.conf.d/*.conf`, which is an INI-style configuration file, where each section is about one daemon or aspect of the NFS service. The old `/etc/defaults/nfs-*` configuration files are still left around, but are unused.

During upgrade, a conversion script is run if the package detects that the `/etc/default/nfs-*` files have been changed. This script is `/usr/share/nfs-common/nfsconvert.py` and it will read the options from `/etc/defaults/nfs-*` and generate `/etc/nfs.conf.d/local.conf`, which overrides the defaults in `/etc/nfs.conf`.

If the conversion script fails for some reason, the package installation or upgrade will fail, and the issue will have to be resolved. Please [file a bug against `nfs-utils` in Launchpad](https://bugs.launchpad.net/ubuntu/+source/nfs-utils/+filebug) if you encounter such a scenario.

A new tool called `nfsconf(8)` can be used to query the configuration settings of `/etc/nfs.conf` and `/etc/nfs.conf.d/*.conf`.

#### Samba server
Samba was updated to 4.15.5, which brings some noteworthy changes. Please see the [upstream release notes for details](https://www.samba.org/samba/history/samba-4.15.0.html), but here are some highlights:

* The development SMB versions SMB2_22, SMB2_24 and SMB3_10 are no longer recognized. SMB2_22 and SMB2_24 should be replaced by SMB3_00, and SMB3_10 should be replaced by SMB3_11
* server multi channel support is no longer experimental
* command-line options in all CLI tooling are now using a common parser, and unknown options which might have been ignored in the past, will now be rejected. See the [upstream release notes](https://www.samba.org/samba/history/samba-4.15.0.html) for details.
* many `/etc/samba/smb.conf` parameters were changed, some removed. Please see the [upstream release notes](https://www.samba.org/samba/history/samba-4.15.0.html) for details.
* the CTDB package was adjusted to work with the new NFS server version shipped in this Ubuntu 22.04
* `findsmb(1)` was removed
* [glusterfs support enabled](https://bugs.launchpad.net/ubuntu/+source/samba/+bug/1894618) in the Ubuntu packaging. This was possible because [glusterfs was promoted to Main](https://bugs.launchpad.net/ubuntu/+source/glusterfs/+bug/1950321) during the 22.04 LTS development cycle, which allowed us to enable the glusterfs vfs module. This module is now present in the `samba-vfs-modules` package.

#### Quagga replaced with frr
`quagga` was removed from Ubuntu 22.04 and replaced by FRRouting (`frr`, https://frrouting.org/).

#### Chrony time synchronization

Chrony has been updated to version 4.2 which includes

 * Add support for AES-CMAC and hash functions in GnuTLS
 * Improve server interleaved mode to be more reliable and support multiple clients behind NAT
 * Add statistics about interleaved mode to serverstats report
 * Adds and enabled further hardening options to the chrony service
 * Allow reading timemaster created configurations
 * For more details read the upstream [release notes](https://chrony.tuxfamily.org/news.html)

#### Virtualization

As usual the release notes can only list a few bigger and more noteworthy changes and packages while
underneath many more components have been updated as well. For an even more complete picture please
have a look at the changelogs of packages and upstream releases of the respective components.

##### qemu

Qemu was updated to version v6.2.0 which brings many major and minor improvements. Among others this version includes:

 * fuse3 based non-root way to [export image files](https://www.qemu.org/2021/08/22/fuse-blkexport/)
 * Jack support for low latency audio
 * Massively improved RISC-V support
 * Many fixes for the emulation of AMD virtualization extensions
 * Improved Power10 support
 * More devices for the microvm build (`virtio-gpu`, `vhost-user-gpu`, `virtio-input-host` and `vhost_user_input`)
 * Allow to remove the additional drivers of `qemu-block-extra`
 * Most common qemu features are now separate modules
 * s390x got improved storage key emulation (e.g. fixed address handling, lazy storage key enablement for TCG, ...)
 * See the upstream changelog for version [6.1](https://wiki.qemu.org/ChangeLog/6.1) and [6.2](https://wiki.qemu.org/ChangeLog/6.2) for an overview of the many further improvements. These also contain a list of suggested alternatives for removed, deprecated and incompatible features.

##### libvirt

Following the regular releases of libvirt version v8.0.0 is now provided in Ubunt 22.04 which includes:

 * Support hotplug and hotunplug for virtiofs
 * Introduce virtio-mem `<memory/>` model
 * qemu: Support librbd encryption
 * qemu: Add new API to inject a launch secret in a domain
 * enhanced swtpm integration (see swtpm below for more)
 * See the upstream [Changelogs](https://libvirt.org/news.html) for the many further improvements and fixes since version 7.6 that was in [Ubuntu 21.10](https://discourse.ubuntu.com/t/impish-indri-release-notes/21951).

##### virt-manager

The new version 4.0.0 of virt-manager is the most recent update after almost 1.5 years without a new upstream version) providing a list of new features:

 * shared memory configuration in the UI
 * virtiofs filesystem driver UI option
 * enable a TPM by default when UEFI is used
 * Use cpu host-passthrough by default on qemu x86
 * use virtio-gpu video for most modern distros
 * More details can be found on the [news page](https://github.com/virt-manager/virt-manager/blob/main/NEWS.md) and individual commits on the [projects website](https://github.com/virt-manager/virt-manager)

##### dpdk

Following the yearly flow of upstream DPDK LTS releases Ubuntu 22.04 contains the most recent DPDK LTS 21.11.
That contains various new device drivers, fixes and optimizations. Even the rather huge [release notes](http://doc.dpdk.org/guides/rel_notes/release_21_11.html) is just about 21.11 itself. Compared to the former DPDK LTS 20.11 that shipped with Ubuntu 21.10 you'd also want to read the DPDK release notes of [21.02](http://doc.dpdk.org/guides/rel_notes/release_21_02.html), [21.05](http://doc.dpdk.org/guides/rel_notes/release_21_05.html) and [21.08](http://doc.dpdk.org/guides/rel_notes/release_21_08.html).

##### openvswitch

The new version 2.17.0 of openvswitch is in Ubuntu 22.04 and provides a general update including the following changes:

 * Various features that ease the use of a userspace datapath.
 * Performance improvements for the OVSDB and clustered OVSDB which is heavily used in OVN deployments.
 * Brings compatibility with DPDK 21.11 (see above).
 * [The OVS News](https://www.openvswitch.org/releases/NEWS-2.17.0.txt) page holds more details about the new version.

##### swtpm

The `swtpm` as well as `libtpms` package is now available and supported in Ubuntu 22.04.

`swtpm` provides TPM emulators with different front-end interfaces to libtpms. TPM emulators provide socket interfaces (TCP/IP and unix) and the Linux CUSE interface for the creation of multiple native /dev/vtpm* devices..

A common use case for `swtpm` is to use it as virtual TPM for virtual machine and container use cases.
This is particular important for guest operating systems that consider TPM support mandatory.

See the [upstream wiki](https://github.com/stefanberger/swtpm/wiki) for more details.

#### Squid

* The `squid` package links against the GnuTLS library.  If you would like to use OpenSSL, you can install the new `squid-openssl` package.

#### cloud-init
                                                                                
Version 22.1 of cloud-init has been released to 22.04, 21.10, 20.04 and 18.04.
                                                                                
Notable features introduced since the last LTS release:
                                                                                
 * Clouds and datasources
   * Add LXD datasource in Jammy which reads dynamic instance data from LXD socket and applies config changes across reboot
   * Added a native VMWare datasource
   * OpenStack and ConfigDrive now support vendor_data2 config overrides
   * Azure boot speed improvements, network config validation and SSH key handling
   * GCE detected earlier in boot
 * Config Modules
   * Add [opt-in hotplug network support via user-data](https://cloudinit.readthedocs.io/en/latest/topics/modules.html#install-hotplug) for OpenStack and ConfigDrive
   * Add deferred write_files config to emit files later in boot
 * Usability
   * Schema validation of `#cloud-config` userdata to annotate specific errors in user-provided configuration

#### ubuntu-advantage-tools

Ubuntu-advantage-tools version 27.8 is released with Jammy.

Notable improvements introduced in this cycle:
 * Service offerings:
     * Ubuntu Pro and Ubuntu Pro FIPS images on Azure, GCP and AWS
     * GCP support to add Ubuntu Advantage licenses to existing VMs
     * AWS support for IPv6 IMDS
     * CIS benchmarks packaged as part of Ubuntu Security Guide (USG)
 * Usability
     * `ua security-status` provides a detailed view of available and applicable package updates provided by Ubuntu proper and Extended Security Maintenance channels
     * Enable Desktop installer to validate and attach Ubuntu Advantage tokens
     * Support machine-readable output JSON/YAML format for most commands
     * Configurable auto attach behavior via `ua attach --attach-config`
### Ubuntu Server Main Promotions
For Ubuntu Server 22.04 LTS, the following source packages were promoted to main:
 * [wireguard](https://www.wireguard.com): fast, modern, secure kernel VPN tunnel
 * [glusterfs](https://www.gluster.org/): cluster file-system capable of scaling to several peta-bytes
 * [frr](https://www.frrouting.org/): suite of internet routing protocols (BGP, OSPF, IS-IS, ...)

### LXD was updated to the new 5.0 LTS version

5.0 LTS significantly steps up LXD’s abilities, especially when operating in clustered environments. In comparison to LXD 4.0, virtual machines are now effectively at feature parity with containers, and a lot of networking options, clustering, and project features were added.

Some of the key changes include:

* **LXD virtual machines** now come with vTPM support as well as arbitrary PCI passthrough support. VMs can now be live-migrated and support some device hotplug and additional storage options.
* **Networking** now includes OVN support combined with BGP, DNS, floating IP and hardware acceleration support.
* **Projects** have grown a number of additional limits and restrictions, making it easy to safely grant access to various teams and limit their resource usage.
* **LXD-migrate** has been reworked with support for both containers and VMs
* **Cluster** users can now perform easy maintenance through cluster evacuation, group servers into target groups and get detailed instance metrics across entire clusters.

Additional details and a complete changelog can be found [here](https://discuss.linuxcontainers.org/t/lxd-5-0-lts-has-been-released/13723).


### Ceph

Ubuntu 22.04 includes the latest release candidate of the Ceph Quincy release.

Ceph packages will be updated as a [stable release update](https://bugs.launchpad.net/ubuntu/+source/ceph/+bug/1968318) once Quincy is released by the Ceph community.

### OpenStack

Ubuntu 22.04 includes the latest OpenStack release, Yoga, including the following components:

* OpenStack Identity - Keystone
* OpenStack Imaging - Glance
* OpenStack Block Storage - Cinder
* OpenStack Compute - Nova
* OpenStack Networking - Neutron
* OpenStack Telemetry - Ceilometer, Aodh, Gnocchi
* OpenStack Orchestration - Heat
* OpenStack Dashboard - Horizon
* OpenStack Object Storage - Swift
* OpenStack DNS - Designate
* OpenStack Bare-metal - Ironic
* OpenStack Filesystem - Manila
* OpenStack Key Manager - Barbican
* OpenStack Load Balancer - Octavia
* OpenStack Instance HA - Masakari

Please refer to the [OpenStack Yoga release notes](https://releases.openstack.org/yoga/) for full details of this release of OpenStack.

OpenStack Yoga is also provided via the [Ubuntu Cloud Archive](https://wiki.ubuntu.com/OpenStack/CloudArchive) for OpenStack Yoga for Ubuntu 20.04 LTS users.

WARNING: Upgrading an OpenStack deployment is a non-trivial process and care should be taken to plan and test upgrade procedures which will be specific to each OpenStack deployment.

Make sure you read the [OpenStack Charm Release Notes](https://docs.openstack.org/charm-guide/latest) for more information about how to deploy and operate Ubuntu OpenStack using Juju.

### needrestart and unattended operations

[needrestart](https://discourse.ubuntu.com/t/needrestart-for-servers/21552) was first installed by default in Ubuntu 21.04 and continues to feature in Ubuntu 22.04. It helps ensure that services are correctly restarted when their dependencies receive security updates.

By default, needrestart will prompt after upgrading packages if restarts are determined to be required. To suppress this behaviour, you can set `DEBIAN_FRONTEND=noninteractive` as usual. needrestart will then fall back to "list only mode". It will be necessary to restart services afterwards, for example by rebooting or invoking `needrestart -ra`.

## Platforms

### Cloud Images :cloud:

#### AWS
* AWS amd64 images use now a GPT partition table and setup a ESP partition to make it possible to use UEFI as boot mode.

#### Oracle
* Jammy Minimal images are available for ARM64 servers on Oracle Cloud Infrastructure. Note that OCI releases images on a fixed cadence, and Jammy release to OCI will be slightly delayed.

### Raspberry Pi :strawberry:

* The first long-term service (LTS) release of the Ubuntu Desktop for Raspberry Pi
* Support for several Pi-specific boards and tools have been added to the archive:
  * All variants of the popular Pimoroni [Unicorn HAT](https://shop.pimoroni.com/products/unicorn-hat?variant=932565325) are now supported with packaging
  * The official DSI touchscreen is now supported (however, see known issues below for a workaround regarding the desktop image)
  * The [rpiboot](https://launchpad.net/ubuntu/+source/rpiboot) package contains the [rpiboot](https://github.com/raspberrypi/usbboot) utility for working with Raspberry Pi Compute Modules (and other Pi boot facilities)
  * The [pyboard-rshell](https://launchpad.net/ubuntu/+source/pyboard-rshell) package contains the [rshell](https://pypi.org/project/rshell/) utility for working with micro-controller boards supporting MicroPython, including the Raspberry Pi Pico
  * The [rpi-imager](https://launchpad.net/ubuntu/+source/rpi-imager) package contains the Raspberry Pi imager utility. The equivalent [snap package](https://snapcraft.io/rpi-imager) has also been updated to operate on all architectures (and bumped to the current version)

### ppc64el

Starting with 22.04 LTS, Ubuntu Server for IBM POWER (ppc64el) is now compiled for Power9 processors using '--with-cpu=power9' ([bug 1930086](https://bugs.launchpad.net/bugs/1930086)).
Thus Ubuntu Server 22.04 LTS will not run, install or even boot on Power8 systems anymore, due to the different instruction set requirements.
Ubuntu Server 20.04 LTS can still be used for Power8 systems for several years - at least until end of base support in April 2025. Users running Ubuntu Server on Power8 today will be prevented from being upgraded to 22.04 LTS using ‘do-release-upgrade’, as this will obviously break such systems ([bug 1960255](https://bugs.launchpad.net/bugs/1960255)).
In addition, Ubuntu Server 22.04 LTS is the first Ubuntu release that comes with official support for IBM Power10 systems.

### s390x

우분투 서버 20.04 LTS (IBM Z와 LinuxONE 지원)에서 부터, 최소 아키텍쳐 레벨 셋은 z13(그리고 LinuxONE Rockhopper / Emperor)로 상향 됐었습니다 - 이는 여전히 우분투 서버 22.04 LTS에 적용 돼 있고 지원 역시 현재(22.04 출시일) 서비스 되고 있는 모든 더 신형의 하드웨어를 포함합니다. 미래 하드웨어에 대한 추가적 지원은 차후에 추가 될 수 있습니다.
우분투 서버 22.04 LTS는 LPAR (classic 또는 DPM 모드)에 IBM z/VM 게스트로, KVM 가상 머신으로 그리고 LXD, docker, kubernetes와 같은 서로 다른 컨테이너 환경으로 설치될 수 있습니다.

21.10부터의 IBM Z와 LinuxONE / s390x 특정 (부분적으로 s390x 만이 아닌) 향상점:

  * 위에서 언급했듯이 22.04 LTS는 OpenSSL 3, 정확히는 v3.0.2([버그 1905022](https://bugs.launchpad.net/bugs/1905022))를 차용한 첫번째 릴리즈이고 이 전환은 몇몇 호환성 문제([버그 1959736](https://bugs.launchpad.net/bugs/1959736)) 때문이며 그 업데이트는 다음 변화를 포함하여 전체 s390x 암호화 스택의 대규모 리뉴얼로 마무리 될 예정입니다:
    * 마침내 libica가 v4.0.1 ([버그 1959421](https://bugs.launchpad.net/bugs/1959421))로 업데이트 됐고 이는 보안 검사([버그 1959553](https://bugs.launchpad.net/bugs/1959553))를 반영하기 위한 확장 통계를 포함합니다
    * openssl-ibmca가 libica4와의 호환성을 위해 결국 2.2.2 ([버그 1958419](https://bugs.launchpad.net/bugs/1958419))로 업데이트 됐습니다 ([버그 1960004](https://bugs.launchpad.net/bugs/1960004)). 
    * opencryptoki가 v3.17.0+dfsg+20220202.b40982efh로 업데이트 되었고 (3.18의 예정된 출시일이 22.04 GA로 공고 됐기 때문) (Bug:1959419) 이는 몇몇 (보안) 수정과 핵심 관리 도구(LP 1959577)에 있는 것과 같은 신기능 들을 포함합니다.
    * 더불어 cryptsetup 또한 업데이트 됐습니다 ([버그 1959427](https://bugs.launchpad.net/bugs/1959427))
s390x와 관련된 추가 업데이트는 다음입니다:
    * libgcyrpt(20)의 최신 v1.9.4로의 업그레이드
    * SIMD 구현을 사용하게 되는 chacha20의 커널 자체 최적화 ([버그 1853152](https://bugs.launchpad.net/bugs/1853152))
    * 새로운 IBM Z 암호화 하드웨어 활용 추가를 위한 zcrypt 디바이스 드라이버 업데이트 ([버그 1959547](https://bugs.launchpad.net/bugs/1959547))
    * 그리고 암호 기반을 위한 인터페이스를 제공하는 마침내 새롭게 패키징 된 IBM Z 보호키 암호화 라이브러리 ([버그 1932522](https://bugs.launchpad.net/bugs/1932522))

  * 추가로 새로운 네트워크 기능들, 이를테면 KVM 설정 향상과 z/OS 상호 운용성을 위한 향상된 HSCI (HiperSockets Converged Interface) 멀티 MAC 지원 같은 기능이 추가되었습니다 (kernel LP: 1932137 그리고 s390-tools LP: 1929721). 그리고 공유 메모리 통신 분야의 중요한 업데이트 이를테면 EID (Enterprise ID) 지원 (kernel LP: 1929060, s390-tools LP: 1929056), SMC 통계 지원 ([버그 1959470](https://bugs.launchpad.net/bugs/1959470)) 그리고 SMC-R v2 지원 ([버그 1929035](https://bugs.launchpad.net/bugs/1929035)) - 그리고 smc-tools 와 함께 최신 v1.7.0로 업그레이드 됐습니다 ([버그 1959428](https://bugs.launchpad.net/bugs/1959428)).

  * 여러 새로운 기능과 연관된 KVM과 보안 실행 역시 안착했고 다음과 같습니다:
    * KVM과 유저 공간에 의해 가로채진 명령어를 위한 스토리지 키 확인 활성화 ([버그 1933176](https://bugs.launchpad.net/bugs/1933176)) ([버그 1933179](https://bugs.launchpad.net/bugs/1933179))
    * 활성된 'access-register mode' ([버그 1933178](https://bugs.launchpad.net/bugs/1933178))
    * QEMU를 위한 긴 커널 명령줄 허용 ([버그 1959984](https://bugs.launchpad.net/bugs/1959984))과 보안 실행 게스트 ([버그 1959985](https://bugs.launchpad.net/bugs/1959985)).
    * 보안 실행 게스트를 위한 GISA를 통해 지원되는 게스트 인터럽트 활성화 ([버그 1959977](https://bugs.launchpad.net/bugs/1959977))
    * 사용자 키를 통한 보안 실행 게스트 덤프 암호화 지원 ([버그 1959965](https://bugs.launchpad.net/bugs/1959965))
    * 그리고 virt-*tools, 특히 virt-manager에서 vfio-ccw와 vifio-ap 활성화 ([버그 1959976](https://bugs.launchpad.net/bugs/1959976))
    * 추가로 KVM_CAP_S390_MEM_OP_EXTENSION 가용성이 211로 판올림 됐고 ([버그 1963901](https://bugs.launchpad.net/bugs/1963901)) KVM이 향상된 체계적 SIGP 컴플라이언스를 갖게 됐습니다 ([버그 1959735](https://bugs.launchpad.net/bugs/1959735)).

  * 새로운 IBM Z 하드웨어 지원을 위해 현대화된 툴체인이 필요 했고 ([버그 1959379](https://bugs.launchpad.net/bugs/1959379)), 22.04 기본 gcc가 v11.2가 됐습니다 (12, 10, 9는 universe에 있습니다).
Binutils이 gdb에 할당 되었고 ([버그 1959407](https://bugs.launchpad.net/bugs/1959407)) v2.38로 ([버그 1959463](https://bugs.launchpad.net/bugs/1959463)), 또 다시 새로운 하드웨어 지원을 추가하기 위해 업데이트 됐습니다 ([버그 1959408](https://bugs.launchpad.net/bugs/1959408)).
그리고 LLVM 역시 새로운 하드웨어 지원을 위해서 ([버그 1959378](https://bugs.launchpad.net/bugs/1959378)), 그리고 향상된 최적화를 포함하기 위해서 업데이트 되었는데 ([버그 1959406](https://bugs.launchpad.net/bugs/1959406)), v14가 기본이더라도 v13만 이용 가능한 것이 아닙니다.

  * glibc로 최신 하드웨어 지원 추가가 ([버그 1959385](https://bugs.launchpad.net/bugs/1959385) 그리고 LP: 1959383) glibc가 최신 v2.35로 업그레이드 되면서 이루어졌고 ([버그 1959429](https://bugs.launchpad.net/bugs/1959429)), 이는 HWCAP_S390_PCI_MIO와 HWCAP_S390_SIE를 포함합니다 ([버그 1959462](https://bugs.launchpad.net/bugs/1959462)).
Perl 호환되는 라이브러리 PCRE2가 v10.39로 업데이트 되었고 s390x와 full JIT 성능 향상을 위한 개선을 포함합니다 ([버그 1959917](https://bugs.launchpad.net/bugs/1959917)).
'Eigen3' 대수학 라이브러리 역시 s390x를 위해 향상된 최적화를 포함하고 ([버그 1884725](https://bugs.launchpad.net/bugs/1884725)) 질의 용량 라이브러리이자 시스템 정보 추출 유틸리티인 'qclib'도 v2.3.0로 판올림 되었습니다 ([버그 1959464](https://bugs.launchpad.net/bugs/1959464)).
마지막으로 애플리케이션에서 Nerual Network Processing Assist Facility (NNPA)를 사용케 하는 인터페이스를 제공하는 새로운 저수준 IBM Z Deep Neural Network Library (zDNN) 라이브러리가 패키징 됐고 현재 이용 가능합니다 ([버그 1959396](https://bugs.launchpad.net/bugs/1959396)).

  * IBM Z를 위한 우분투 서버의 핵심 컴포넌트는 s390-tools 패키지이고 이는 jammy의 5.15 커널 배치에 맞춰져 v2.2.0로 업그레이드 되었으며 ([버그 1959420](https://bugs.launchpad.net/bugs/1959420)), 이제 환경 블록과 함께 다른 기능을 포함하는데 ([버그 1959409](https://bugs.launchpad.net/bugs/1959409)), 이 컴포넌트는 다중 경로 re-IPL 기능([버그 1959546](https://bugs.launchpad.net/bugs/1959546)), DPM 시스템을 위해 PCI 장치를 자동 활성화 해주는 옵션인 IPL 레코드의 필요없이 부팅 중에 평가되는 영구적인 설정 정보입니다 ([버그 1959537](https://bugs.launchpad.net/bugs/1959537)).

  * 커널 기반의 새로운 IBM Z 하드웨어 지원 ([버그 1960187](https://bugs.launchpad.net/bugs/1960187)), 새로운 하드웨어를 위한 새로운 CPU-MF 계수기([버그 1960117](https://bugs.launchpad.net/bugs/1960117)), s390x에서의 긴 커널 명령줄 지원 ([버그 1960580](https://bugs.launchpad.net/bugs/1960580)), 투명한 PCI 장치 복구 지원 ([버그 1959532](https://bugs.launchpad.net/bugs/1959532)), HBA 펌웨어에서의 향상된 유저 정보 ([버그 1959545](https://bugs.launchpad.net/bugs/1959545)) 그리고 CONFIG_QETH_OSX 커널 설정 옵션 비활성화의 삭제와 마찬가지로 커널이 몇몇 s390x 향상 역시 얻었습니다. 
  
  * 서비스 호출 논리 프로세서 (SCLP) 콘솔 인터페이스 드라이버 ('운영체제 메시지' 줄 모드와 '통합 ASCII 콘솔' VT220을 위함)가 모든 sclp 요청이나 그저 실패하는 sclp 요청을 로깅하기 위해서 두 가지 디버그 기능을 얻었고, 이는 커널을 ([버그 1960435](https://bugs.launchpad.net/bugs/1960435)) s390 도구 변경과 마찬가지로 필요로 합니다 ([버그 1960437](https://bugs.launchpad.net/bugs/1960437)).

### RISC-V

Starting with 22.04 LTS, besides the standard device-specific preinstalled image, we now also provide a live installer image for the RISC-V architecture. This can be helpful when wanting to install Ubuntu on an NVMe drive on an Unmatched board, for instance.

### UEFI and BIOS boot

Other operating systems are not displayed in the boot menu anymore, unless Ubuntu has been installed alongside another operating system. Once all other operating systems are removed from the machine, detection of other operating systems is disabled, and to re-enable if after installing another OS, you will have to delete `/boot/grub/grub.cfg` and immediately run `update-grub` again.

# Known Issues

As is to be expected, with any release, there are some significant known bugs that users may run into with this release of Ubuntu. The ones we know about at this point (and some of the workarounds), are documented here so you don’t need to spend time reporting these bugs again:

## Linux kernel

Nothing yet.

## Security
* OpenSSL 3.0.2 doesn't work with the [Turkish locale](https://launchpad.net/bugs/1968997).  To work around this issue until a fix is available, affected users are advised to set LC_CTYPE=C.UTF-8 in their environment for processes that use openssl (at a shell: `export LC_CTYPE=C.UTF-8`).  This will break capitalization of strings according to rules for the Turkish language, so is not recommended to be overridden at the system level.

## System
* systemd / journald now defaults to `zstd` compression and uses the “keyed hash” feature (upstream default as of v246). Therefore, journal files written on Ubuntu 22.04 (using systemd v249) cannot be opened using an older version of journal (i.e. from a 18.04/20.04/Core20 installation). This will fail with an error ([LP: #1953744](https://bugs.launchpad.net/subiquity/+bug/1953744), [forum.snapcraft.io](https://forum.snapcraft.io/t/accessing-journal-logs-from-22-04-hosts-when-using-older-base-snap/29627)):
    ```
    Journal file xxx.journal has unknown incompatible flags 0xc
    Failed to open journal file xxx.journal: Protocol not supported
    ```
* Users of grub-customizer could hit [a bug](https://pad.lv/1969353) in the late stage of the upgrade process leading to the final stage of the upgrade to fail (autoremoval of packages). A workaround is available [in the bug's comments](https://bugs.launchpad.net/ubuntu/+source/ubuntu-release-upgrader/+bug/1969353/comments/6).

## Ubuntu Desktop

* The Ubuntu Desktop images can be slow to boot (taking up to 10 minutes) when booted from a USB drive on a BIOS system. The issue is being [investigated](https://bugs.launchpad.net/ubuntu/+source/casper/+bug/1922342), however once the system is installed this is not an issue.
* The Ubuntu Desktop images can be very slow to boot (taking up to 30 minutes) when booted from optical media (DVD) on a a BIOS or UEFI system. This is due to an integrity checker being run against the installation media. A workaround (setting "fsck.mode=skip") is documented in [the relevant bug](https://bugs.launchpad.net/ubuntu/+source/casper/+bug/1930880).
* A hang of the Ubuntu Desktop installer, Ubiquity, [has been observed](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1946828),  where it is scanning NTFS partitions to determine if they can be resized.  The symptom of this is a spinning ball cursor when attempting to continue past the installer 'Updates and other software' screen.  If this occurs, please reboot and try again.
* The Firefox snap does not support the [NativeMessaging protocol](https://launchpad.net/bugs/1741074) yet but this feature is planned to be added soon. This means for instance that installing GNOME Shell extensions from Firefox won't work. As a workaround, you can try the `gnome-shell-extension-manager` app.
 * Brazilians (and others that need PKCS#11 smartcard support in Firefox) **should not upgrade to Jammy** until [pkcs#11 support is added to the firefox snap](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1967632)
* The GNOME Tweaks app no longer manages GNOME Shell extensions. You can install `gnome-shell-extension-manager` instead.
* There isn't an option to use Wayland for systems with [Nvidia graphics drivers](https://launchpad.net/bugs/1968929).
* To use AppImages, you'll first [need to run](https://launchpad.net/bugs/1965636) `sudo apt install libfuse2`
* RDP (Remote Desktop) Sharing [appears on](https://launchpad.net/bugs/1969619) by default but it is not on and needs to be turned off and then turned on to enable.
* An upgrade to Ubuntu 22.04 LTS can cause [a bad interaction between snapd and update-notifier](https://bugs.launchpad.net/ubuntu/+source/snapd/+bug/1969162) which can cause the upgrade to hang. The fix is currently in flight and upgrades will be enabled shortly.

## Ubuntu Server

* Due to a [current issue with fallocate on zfs](https://bugs.launchpad.net/ubuntu/+source/zfs-linux/+bug/1969247), mysql fails to install on Jammy zfs systems 

## Platforms

### Cloud Images

#### Vagrant
* Jammy `vagrant` from `universe` does not support openssl3 upstream. This will cause users of vagrant on a Jammy host to receive OpenSSL errors on start. The box will still be booted, and `vagrant ssh` will operate, however `vagrant` functionality will be severely impacted. Connections between boxes will not operate normally. [bug report.](https://bugs.launchpad.net/ubuntu/+source/vagrant/+bug/1964025)
* Vagrant < 2.216 will fail to launch due to SSH connection issues. `vagrant`, as provided in the Ubuntu archives, does not reach >= 2.2.16 until Jammy .  One workaround is to use an upstream version of `vagrant` on your system. [Upstream bug, already fixed.](https://github.com/hashicorp/vagrant/issues/11783).  The Cloud Team is also working on a more permanent solution: [Public cloud-images bug](https://bugs.launchpad.net/cloud-images/+bug/1969664)

### Raspberry Pi

* The Raspberry Pi desktop images have switched to using the Full KMS graphics drivers. The official Raspberry Pi DSI display does not work with full KMS enabled. To enable the use of the Raspberry Pi DSI display, edit the `config.txt` file on your Raspberry Pi's hard drive and change the line `dtoverlay=vc4-fkms-v3d` to `dtoverlay=vc4-kms-v3d`
* Currently, the USB ports on the official IO board for the Compute Module 4 are inoperative ([bug 1969689](https://launchpad.net/bugs/1969689))
* On the desktop image, the Firefox snap can take some time (several minutes has been noted) to complete initialization after first login ([bug 1969529](https://launchpad.net/bugs/1969529))
* The legacy camera stack (MMAL based) is no longer supported on `arm64`; [libcamera] is the supported method of using the Pi Camera Module on the `arm64` architecture (the boot-time configuration will automatically load overlays for detected modules)

Carried over from interim releases (these are changes are applicable from LTS->LTS):

* After initial user setup on the desktop image, several packages can still be autoremoved ([bug 1925265](https://launchpad.net/bugs/1925265)); run `sudo apt autoremove` to work around this
* On the desktop image, the wrong audio output device is selected on each boot. A workaround is available in the bug report ([bug 1899962](https://launchpad.net/bugs/1899962))
* Various kernel modules have been moved from the `linux-modules-raspi` package in order to reduce the initramfs size. If you find an application failing due to missing kernel modules, please try the following:
  * `sudo apt install linux-modules-extra-raspi`

### s390x

No known issues yet.

# Official flavours

The release notes for the official flavours can be found at the following links:

* [Kubuntu Release Notes](https://wiki.ubuntu.com/JammyJellyfish/ReleaseNotes/Kubuntu)
* [Lubuntu Release Notes](https://discourse.lubuntu.me/t/lubuntu-22-04-lts-jammy-jellyfish-release-notes/3179)
* [Ubuntu Budgie Release Notes for 21.10 upgraders](https://ubuntubudgie.org/2022/03/ubuntu-budgie-22-04-lts-release-notes/) & [Ubuntu Budgie Release Notes for 20.04 upgraders](https://ubuntubudgie.org/2022/04/ubuntu-22-04-release-notes-for-20-04-upgraders/)
* [Ubuntu Kylin Release Notes](https://wiki.ubuntu.com/JammyJellyfish/ReleaseNotes/UbuntuKylin)
* [Ubuntu MATE Release Notes](https://ubuntu-mate.org/blog/ubuntu-mate-jammy-jellyfish-release-notes/)
* [Ubuntu Studio Release Notes](https://ubuntustudio.org/ubuntu-studio-22-04-lts-release-notes/)
* [Xubuntu Release Notes](https://wiki.xubuntu.org/releases/22.04/release-notes)

# More information

## Reporting bugs

Your comments, bug reports, patches and suggestions will help fix bugs and improve the quality of future releases. Please [report bugs using the tools provided](http://help.ubuntu.com/community/ReportingBugs). If you want to help out with bugs, the [Bug Squad](http://wiki.ubuntu.com/BugSquad) is always looking for help.

## Participate in Ubuntu

If you would like to help shape Ubuntu, take a look at the list of ways you can participate at:

* https://community.ubuntu.com/contribute

## More about Ubuntu

You can find out more about Ubuntu on the [Ubuntu website](https://www.ubuntu.com).

To sign up for future Ubuntu development announcements, please subscribe to Ubuntu’s development announcement list at:

* https://lists.ubuntu.com/mailman/listinfo/ubuntu-devel-announce
