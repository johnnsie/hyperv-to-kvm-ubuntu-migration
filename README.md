# Hyper-V (VHDX) → KVM (QCOW2) Ubuntu Migration Playbook

This repository contains a **complete, real-world recovery and migration runbook** for restoring **Ubuntu virtual machines** from **Microsoft Hyper-V Gen2 (UEFI)** into **KVM/libvirt** on Ubuntu hosts.

This is **not a happy-path guide**.

It documents **every command and intermediary step** required during an actual migration, including the failure modes that are typically skipped or glossed over in other guides.

---

## Why this exists

Most Hyper-V → KVM guides assume:
- BIOS boot
- Clean shutdowns
- Matching hardware
- Working GRUB
- Stable networking

In reality, Gen2 Hyper-V Ubuntu VMs almost always fail on first boot under KVM.

This playbook exists to make that failure **predictable, recoverable, and repeatable**.

---

## What this guide explicitly covers

This repository documents, end-to-end, how to recover from:

- **UEFI boot loops after import**
- **Missing EFI variables (`efivarfs`)**
- **Mandatory GRUB reinstall**
- **ISO cold-attach limitations in libvirt**
- **EFI Shell behavior and `grubx64.efi` loopbacks**
- **Installer → Rescue → chroot recovery workflow**
- **LVM with separate `/boot` and EFI partitions**
- **Netplan interface renaming (`eth0` → `enp1s0`)**
- **Serial console enablement to avoid VNC permanently**

Every one of these issues occurred during a real migration and is fully documented.

---

## Project goal

The goal of this project is **repeatable disaster recovery**, not theoretical migration.

You should be able to:
- Take an arbitrary Ubuntu Hyper-V Gen2 VHDX
- Convert it
- Import it
- Fix every expected failure
- End with a booting, reachable VM

**Every time.**

---

## Who this is for

- **Sysadmins** migrating workloads off Hyper-V
- **Homelab operators** restoring VHDX backups
- **Infrastructure engineers** performing cross-hypervisor recovery
- Anyone recovering **Ubuntu Gen2 VMs** into KVM/libvirt

---

## What’s included

- 📘 **Full command-by-command migration playbook**
  - `FULL_PLAYBOOK.md`
  - `FULL_PLAYBOOK.pdf` (printable, DR-binder ready)
- 🧩 **Example configurations**
  - Netplan interface fix
  - libvirt OVMF firmware snippet
- 📜 **MIT License**
  - Unrestricted reuse in homelabs and enterprise environments

---

## When to use this guide

If your imported Ubuntu VM:

- Drops straight into **UEFI**
- Loops endlessly on boot
- Refuses to boot disk
- Boots the installer instead of the OS
- Loses networking after migration

👉 **This guide fixes it.**

---

## License

MIT — see [`LICENSE`](LICENSE)

Use it, fork it, modify it, publish it internally.
