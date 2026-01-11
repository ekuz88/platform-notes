# Prepare Linux VM for VS Code Remote SSH

Minimal steps to prepare a Linux virtual machine for connecting with
Visual Studio Code using the Remote SSH extension.

> Commands are written for AlmaLinux and other RHEL-compatible,
> DNF-based distributions (AlmaLinux, Rocky Linux, RHEL, Fedora).

---

## Prerequisites

- Linux VM
- SSH access
- Non-root user with a home directory

---

## System update

```bash
sudo dnf update
```

Ensure system packages are up to date.

---

## Required utilities

VS Code Server is unpacked on the remote host.

```bash
sudo dnf install tar unzip --setopt=tsflags=nodocs
```

---

## Home directory execution

VS Code Server runs from `~/.vscode-server`.
If `/home` is mounted with `noexec`, it must be remounted.

```bash
sudo mount -o remount,exec /home
```

For permanent setup, adjust `/etc/fstab`.

---

## Workspace directory

```bash
mkdir -p ~/src
```

Recommended location for source code and repositories.

---

## SSH key for GitHub

Generate an Ed25519 SSH key.

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

Show the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Add it to GitHub:
Settings → SSH and GPG keys.

---

## Git identity (local)

Configure Git identity for repositories on this VM.

```bash
git config user.name "Your Name"
git config user.email "your.email@example.com"
```

---

## Verification

```bash
ssh user@vm_ip
```

If SSH works, VS Code Remote SSH should connect successfully.

---

## Notes

- No VS Code packages are required on the VM
- VS Code Server is managed by the client
- Do not run VS Code Server as root
