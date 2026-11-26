# Linux-Ops-Server

![Status](https://img.shields.io/badge/status-in%20progress-yellow)

Ansible automated configuration and hardening of a fresh Ubuntu 24.04 server: SSH, firewall, patching, monitoring, and tested backup/restore.

## Overview

One playbook takes a freshly installed Ubuntu Server 24.04 LTS to a hardened, monitored, backed up state. Every role is idempotent (a second run reports `changed=0`), secrets live in Ansible Vault, and recovery is tested rather than assumed.

**Environment:** Mac mini running Ubuntu Server 24.04 LTS as the managed server, with a separate machine as the Ansible control node.

## Roles

| Role | What it does | Status |
|---|---|---|
| `common` | Admin user with sudo, base packages, timezone and NTP, hostname, static IP | ⬜ |
| `ssh_hardening` | Key-only login, root login disabled, `AllowGroups`, login banner | ⬜ |
| `firewall` | `ufw` default-deny inbound; allows SSH and monitoring ports | ⬜ |
| `patching` | Unattended security updates; on-demand patch playbook that reboots only when required | ⬜ |
| `logging` | journald retention, logrotate rules | ⬜ |
| `monitoring` | Netdata as a systemd service, with a disk-over-85% alert | ⬜ |
| `backups` | restic backups with retention rules, run by a systemd timer | ⬜ |

## Validation

| Test | Result |
|---|---|
| Full rebuild from bare Ubuntu install | _TBD_ |
| Idempotency: second run of `site.yml` | _TBD (target: `changed=0`)_ |
| Restore test: delete a directory, restore with restic | _TBD_ |
| Mock incident: break a service, diagnose, fix, write up | _TBD_ |
| Lynis hardening score | _TBD (before → after)_ |