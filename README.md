# Ansible Playbook: Upgrade Multiple Packages on RPM and DEB Distributions

## Overview
This Ansible playbook upgrades a predefined list of packages on both Debian-based and Red Hat–based Linux distributions.

It performs the following actions:
- Updates the package manager cache
- Displays package versions **before** upgrade
- Upgrades only existing packages to the latest available version
- Displays package versions **after** upgrade

The playbook is safe for mixed environments and avoids installing
new packages unintentionally.

---

## Supported Operating Systems
- Ubuntu / Debian (APT)
- Red Hat Enterprise Linux / CentOS / Rocky / Alma
  - RHEL 7 (YUM)
  - RHEL 8+ (DNF)

---

## Playbook Details
- Hosts: All (*)
- Privilege Escalation: Enabled
- Become Method: sudo
- Become User: root
- Error Handling: ignore_errors enabled to prevent failures

---

## Configurable Variables
The list of packages to be upgraded can be modified in the playbook:

---

### upgrade_packages:
- curl
- open-vm-tools
- python3

Add or remove package names as required.

---

## Tasks Description

### Ubuntu / Debian Section
- Updates APT cache
- Shows current installed versions using `apt-cache policy`
- Upgrades packages using `apt` with `only_upgrade`
- Displays versions after upgrade

### Red Hat Section
- Updates YUM or DNF cache based on OS version
- Shows installed versions using `rpm -q`
- Upgrades packages using YUM or DNF
- Ensures only already-installed packages are upgraded
- Displays versions after upgrade

---

## Use Cases
- Controlled package upgrades before OS patching
- Pre-maintenance or pre-reboot validation
- Standardized upgrades across mixed Linux environments
- Automation pipelines and compliance checks

---

## How to Run
ansible-playbook -i hosts upgrade_packages.yml --ask-pass --become --ask-become-pass -e "ansible_user=username"

---

## Requirements
- Ansible installed on the control node
- SSH access to target hosts
- Sudo/root privileges on managed nodes
- Fact gathering enabled

---

## Notes
- `ignore_errors` is intentionally used to allow execution to continue
  even if a package is missing or unavailable.
- The playbook upgrades **only existing packages** and does not install
  new ones.
- Package versions are displayed before and after upgrade for validation.

---

