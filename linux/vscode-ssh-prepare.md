# Prepare Linux VM for VS Code Remote SSH

Minimal steps to prepare a Linux virtual machine for connecting with\
Visual Studio Code using the Remote SSH extension.

> Commands are written for AlmaLinux and other RHEL-compatible,\
> DNF-based distributions (AlmaLinux, Rocky Linux, RHEL, Fedora).

------------------------------------------------------------------------

## Prerequisites

-   Linux VM
-   SSH access
-   Non-root user with a home directory

------------------------------------------------------------------------

## System update

``` bash
sudo dnf update
```

Ensure system packages are up to date.

------------------------------------------------------------------------

## Required utilities

VS Code Server is unpacked on the remote host.

``` bash
sudo dnf install tar unzip --setopt=tsflags=nodocs
```

------------------------------------------------------------------------

## Install Git

Install Git for working with repositories.

``` bash
sudo dnf install git --setopt=tsflags=nodocs
```

------------------------------------------------------------------------

## Home directory execution

VS Code Server runs from `~/.vscode-server`.\
If `/home` is mounted with `noexec`, it must be remounted.

``` bash
sudo mount -o remount,exec /home
```

For permanent setup, adjust `/etc/fstab`.

------------------------------------------------------------------------

## Workspace directory

Create a directory for source code and repositories.

``` bash
mkdir -p ~/src
```

Recommended location for working repositories.

------------------------------------------------------------------------

## Git identity (global)

Configure Git identity for repositories on this VM.

``` bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Using `--global` ensures the configuration applies to all repositories
for the current user.

------------------------------------------------------------------------

## SSH key for GitHub

Generate an Ed25519 SSH key.

``` bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

Show the public key:

``` bash
cat ~/.ssh/id_ed25519.pub
```

Add it to GitHub:

Settings → SSH and GPG keys

------------------------------------------------------------------------

## SSH permissions (recommended)

Ensure correct permissions for the `.ssh` directory and keys.

``` bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
```

------------------------------------------------------------------------

## Verification

``` bash
ssh -T git@github.com
```

Confirm that SSH access to the VM works correctly.
