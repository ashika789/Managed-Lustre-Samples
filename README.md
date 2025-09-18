# Managed-Lustre-Samples

This repository contains scripts to help automate connecting GCE VMs (Rocky/RHEL 8-based) to Google Cloud Managed Lustre.

There are two primary methods provided:

1.  **`setup_lustre_client.sh` (Recommended):** A universal setup script that you run *inside* each new VM to configure it manually. This is the most reliable method.
2.  **`Auto connect to Lustre from VM` (VM-to-VM Automation):** An automation script you run from *one* admin VM to configure *other* VMs. This is faster but requires specific IAM setup to work.

---

## 1. Universal Manual Script (`setup_lustre_client.sh`)

This is the most reliable method. It's a single script you run manually **inside** any new VM you want to connect to Lustre.

### What it Does
* Takes the Lustre mount point as an argument.
* Adds the official Google Cloud Lustre repository.
* Installs the required client packages (`kmod-lustre-client` and `lustre-client`).
* Creates the `/mnt/lustre` directory.
* Mounts the Lustre drive.
* Adds the drive to `/etc/fstab` to make it automatically re-mount if the VM reboots.

### Usage Workflow

For any new VM you want to connect (e.g., a new VM named `VMToConnect`):

**1. SSH Into Your New VM**
First, connect to your target VM.

```bash
# Example using your project's internal DNS pattern:
ssh your_user@nic0.VMToConnect.your-zone.c.your-project.internal.gcpnode.com