# Hyper-V (VHDX) → KVM (QCOW2) Ubuntu Migration Playbook

This repository contains a **complete, real-world recovery and migration runbook**
for restoring **Ubuntu virtual machines** from **Microsoft Hyper-V Gen2 (UEFI)**
into **KVM/libvirt**.

This is **not a happy-path guide**. It documents every command and intermediary
recovery step required during an actual migration.

If your imported Ubuntu VM:
- Drops into UEFI
- Loops endlessly
- Refuses to boot disk

**This guide fixes it.**
