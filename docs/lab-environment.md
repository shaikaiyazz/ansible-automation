# Lab Environment

## Topology

| VM | Role |
|---|---|
| `cnode` | Ansible control node |
| `mac1` | Managed node in `dev` |
| `mac2` | Managed node in `test` |

## Software baseline

- Red Hat Enterprise Linux 10.3
- Ansible Core 2.16.19
- Python 3.12.15

## Pre-flight checklist

1. Confirm `mac1` and `mac2` resolve from `cnode`.
2. Confirm SSH authentication works for the configured remote user.
3. Confirm the remote user has sudo privileges.
4. Update `inventory/hosts.ini` with the correct account.
5. Check the target group before running a playbook.

Do not publish private IP addresses, credentials, host keys or private keys unless you deliberately intend them to be public.
