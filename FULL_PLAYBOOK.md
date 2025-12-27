# Hyper-V → KVM Ubuntu Migration (FULL COMMAND PLAYBOOK)

This document records **every command required**, with no skipped steps.

## 0. Host Preparation
sudo apt update
sudo apt install -y qemu-kvm libvirt-daemon-system libvirt-clients virtinst virt-manager   qemu-utils libguestfs-tools ovmf
sudo systemctl enable --now libvirtd

## 1. Repair and Convert VHDX
qemu-img check -r all source.vhdx
qemu-img convert -p -O qcow2 source.vhdx vm.qcow2

## 2. Inspect Disk Layout
virt-filesystems -a vm.qcow2 --all --long -h

## 3. Create VM (Import Mode)
virt-install --import   --name vm-name   --memory 4096   --vcpus 2   --cpu host   --disk path=/srv/vms/vm.qcow2,format=qcow2,bus=virtio   --os-variant ubuntu22.04   --network network=default,model=virtio   --graphics none

## 4. Force UEFI Firmware (OVMF)
See examples/virsh-ovmf.xml
