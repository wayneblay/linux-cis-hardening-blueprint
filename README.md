# Linux CIS Hardening Blueprint

A step-by-step hardening guide for **RHEL 9** and **Ubuntu 22.04 / 24.04 LTS** servers, aligned to the **CIS Benchmark Level 1 – Server** profile.

Every command is tagged for the distribution it applies to, so one document covers both platforms.

**→ [Read the blueprint](CIS-Hardening-Blueprint-RHEL-Ubuntu.txt)**

## What it covers

| Phase | Area |
|------:|------|
| 0  | Pre-flight: backups, snapshot, safety session, baseline scan |
| 1  | Partitions and mount options (`nodev`, `nosuid`, `noexec`), LUKS2 |
| 2  | Package signing, patching, automatic security updates |
| 3  | GRUB password, kernel command line, bootloader permissions |
| 4  | Kernel and network `sysctl` hardening, core dumps |
| 5  | System-wide crypto policy (RHEL) |
| 6  | SELinux (RHEL) / AppArmor (Ubuntu) |
| 7  | Disabling unused filesystems, protocols and USB storage |
| 8  | Removing legacy services, time sync, cron and `at` permissions |
| 9  | Login banners |
| 10 | OpenSSH server hardening |
| 11 | PAM: password quality, lockout, history, aging, umask, sudo, `su` |
| 12 | Host firewall: firewalld (RHEL) / ufw (Ubuntu) |
| 13 | journald, rsyslog and central log forwarding |
| 14 | auditd configuration and the full CIS audit rule set |
| 15 | File permissions and account hygiene checks |
| 16 | Automated scanning: OpenSCAP (RHEL), Ubuntu Security Guide (Ubuntu) |
| 17 | AIDE baseline, immutable audit rules, reboot and verification |

An **Exceptions** section at the end lists known conflicts (container hosts, routers, Azure, snaps, bastion hosts) so you can document deviations instead of breaking things.

## How to read the tags

| Tag | Meaning |
|-----|---------|
| `[ALL]` | Same command on RHEL and Ubuntu |
| `[RHEL]` | RHEL 9 only (Rocky / Alma 9 also apply) |
| `[UBUNTU]` | Ubuntu 22.04 / 24.04 only |
| `[L1]` | CIS Level 1 Server control |
| `[L2]` | CIS Level 2 control — stricter, more operational impact |
| `[REC]` | Recommended practice, not a scored CIS control |

## Before you start

- **Test on a non-production host or snapshot first.**
- **Keep console access** (hypervisor console, iLO/iDRAC, cloud serial console). The SSH, PAM, sudo and firewall phases can lock you out if a step is skipped.
- **Keep a second logged-in session open** until you've confirmed you can open a new SSH session.
- Work through the phases **in order**. AIDE and the immutable audit rules are intentionally last.

## Usage

The blueprint is meant to be read and applied phase by phase, not run as a single script. Copy commands for your distribution, review them against your environment, and check each verification step before moving on.

For automated remediation, Phase 16 shows how to generate a reviewable Ansible playbook (RHEL) or fix script (Ubuntu) from the official scanner content.

## Disclaimer

This project is not affiliated with or endorsed by the Center for Internet Security (CIS). "CIS" and "CIS Benchmarks" are trademarks of the Center for Internet Security, Inc. This guide maps to CIS recommendations in its own words; it does not reproduce benchmark text. Verify control IDs and values against the licensed CIS Benchmark version your auditors use.

The material is provided as-is, without warranty. You are responsible for testing changes before applying them to production systems.

## License

[MIT](LICENSE)
