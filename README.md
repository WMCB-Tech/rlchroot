[![Discord](https://img.shields.io/discord/591914197219016707.svg?label=&logo=discord&logoColor=ffffff&color=7389D8&labelColor=6A7EC2)](https://discord.gg/vpEv3HJ)      [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) [![Open Source? Yes!](https://badgen.net/badge/Open%20Source%20%3F/Yes%21/blue?icon=github)](https://github.com/Naereen/badges/)

# rlchroot - RootLess Chroot
RLChroot (RLC) Allows you to install Linux distros on your Android device without rooting, giving an LXC Like Interface inspired by [Udocker](https://github.com/indigo-dc/udocker)

> rlchroot is just a chroot manager for Termux but it has templates configuration allows you to easily install distros pre-defined, users can manually setup distros on their own without template configs at all

### Supported Distros
The only distros that i can maintain is the subset of distros (`Ubuntu`, `Debian`, `Kali`, `Alpine`, `Arch Linux`), each of them has releases supported (see `rlc-create list` command)

Note that newer distros have bugs so please file a bug report

Here are the distros we're planning to add:
* Devuan
* Fedora
* Void
* Linux Mint
* Gentoo
* Parrot OS

### Do i need Cgroups, VETH, seccomp?
RLChroot isn't nearly that complex as LXC/LXD does, `rlchroot` uses `proot` for chrooting, it uses `ptrace()` and does not use cgroups, veth and seccomp or any PAM Modules, as it uses host resources and limitations may occur, see below

# Installation
Enter the following commands to install rlchroot
```
echo "deb [trusted=yes arch=all] https://wmcb-tech.github.io/files termux universe" >> $PREFIX/etc/apt/sources.list.d/rlchroot.list
pkg up && pkg in rlchroot
```

If you can't use `apt` or you want to use older versions, you can go to [Releases](https://github.com/WMCB-Tech/rlchroot/releases) page

# RLC Commands
Here are the commands that is available, and others will be implemented in the future, for now here are the commands that is available:
* `rlc-create`
* `rlc-destroy`
* `rlc-ls`
* `rlc-launch`
* `rlc-import`
* `rlc-export`

Here are the commands that needs to fleshed out in the future:
* `rlc-snapshot` - Sure there's an import and export commands
* `rlc-freeze` and `rlc-unfreeze` - Minimal Freeze (Using SIGSTOP)
* `rlc-download`
* `rlc-info`

Pull Requests are welcome to implement these commands

### Setting up your first container
I assume you setup Ubuntu 18.04 Container, to setup Ubuntu 18.04 container, create a container with `rlc-create` command
```
rlc-create bionic mycontainer
```
The *mycontainer* is the name of your container

Or to setup Kali Container, type:
```
rlc-create kali my-kali-container
```

It will configure the container for you

---

To start the container, type:
```
rlc-launch mycontainer
```

Alternatively. to run a command from container, run:
```
rlc-launch mycontainer mycommand
```

You can list your installed container with `rlc-ls` command

---

To run the container as non-rooted, rlc already configures that for you with sudo access, run
```
rlc-launch mycontainer su - user
```

Or if you want to use commands as user, do
```
rlc-launch mycontainer sudo -i -u user mycommand
```

If you want to add user account, you may use `useradd` or `adduser` command

### Destroying the Container
If you don't want to use your container anymore or is broken, run:
```
rlc-destroy mycontainer
```

And it will ask you to delete your container

# Limitations
While `proot` can only emulate chroot, the limitations is that you won't be able to do low-level admin access, including creating chroots, mounting images, creating device nodes or access devices. this is all thanks to android security features so don't expect VPN or Networking stuff

Features lacks include:
* Full Namespaces (Only minimal namespace)
* Virtio Interface
* Full cgroups support
* Seccomp Support

# Security
While rlchroot does not require cgroups or extra layers of security. you may still get into trouble including stolen passwords, ~~gaining access to your host partition, by default, rlchroot mounts your `/sdcard` `/system` and `/data` partition so be careful on what you're doing as you break stuff~~ Mounted Partitions can be configured in `$PREFIX/var/rlc/mountpoints.conf`

# Contributing
Contributions are welcome, you may create PR's, submit a bug report and create a Feature Requests
