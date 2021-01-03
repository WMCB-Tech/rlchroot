# rlchroot (beta)
RLChroot - Install Linux Distro without root, giving an LXC-Like Interface for Android, Linux and Non-Privileged Users

# What's This?
RLChroot Stands for (RootLess Chroot) giving the lxc-like commands (inspired by [udocker](https://github.com/indigo-dc/udocker)) for Termux without root \
With all that said, you can manage your distros individually and do anything with them

To run such distros, we use `proot` for rootless chroot management

### Supported Distros
For now, i will maintain a subset of distros that is based on debian which is (Ubuntu, Debian, Kali)

Each of their releases has it's own version (see `rlc-create list` command)

### Do i need cgroups, veth, seccomp?
`rlchroot` is not nearly complex as LXC/LXD does but it has the features the same as lxc but only minimal for now, see below

# Installation
1. Download the [Debian Package file](https://github.com/WMCB-Tech/rlchroot/releases/tag/1.01) for Termux
2. Install the Debian Package file with `dpkg` or `apt` (`apt install ./path/to/rlchroot.deb`)

# RLChroot Commands
Here are the commands are present for now and we are working on fleshing out some commands
* `rlc-create` - Creates the Distro and installs it from their templates
* `rlc-launch` - Launches the Container
* `rlc-destroy` - Destroys the Container
* `rlc-ls` - Lists all the Installed Containers
* `rlc-import` - Imports the container
* `rlc-export` - Exports the Container

Here are the commands that we're working on in the future
* `rlc-snapshot` - Sure there's a `rlc-import` and `rlc-export` command
* `rlc-freeze` - Minimal Freeze (Using SIGSTOP)
* `rlc-copy`
* `rlc-download`
* `rlc-file-push`
* `rlc-file-pull`

# Setting up your first container
I would suggest Ubuntu 18.04, however a list of distros can be listed in `rlc-create list` command

To Install the container (Ubuntu 18.04), Type: \
`rlc-create bionic container1`

Or To install debian 10, type: \
`rlc-create buster debian-name`

Synopsis: \
`rlc-create [DISTRO_NAME] [CONTAINER_NAME]`

*Other distros may fail to install, please file a bug report*

# Running your container
To run your container, type: \
`rlc-launch [CONTAINER_NAME]`

To pass commands from the container, use: \
`rlc-launch [CONTAINER_NAME] [COMMAND]`

To login as `user`, use: \
`rlc-launch [CONTAINER_NAME] su - user`

*The `user` command is already configured for you*

Once you loggined in to the container, your home directory is synced from your host, here are the bind-mounted partitions from host:
* `/tmp` = `$PREFIX/tmp`
* `/home/user` = `$HOME`
* `/root` = `$HOME`

# Deleting your Container
You can delete your container by typing: \
`rlc-destroy [CONTAINER_NAME]`

# Can i contribute?
Yes, you can contribute by filing a bug report, PR's and much more
