# Ansible Automation Labs

A practical portfolio of Ansible automation exercises for Linux infrastructure administration.

> **Lab baseline:** RHEL 10.3, Ansible Core 2.16.19 and Python 3.12.15.  
> **Topology:** `cnode` (control node), `mac1` and `mac2` (managed nodes).

## What this project demonstrates

- Inventory and host-group management
- Connectivity checks
- Package and service management
- Linux group, user and directory management
- Directory permissions and SGID
- Secure secret-handling practices with Ansible Vault

## Repository layout

```text
.
├── ansible.cfg
├── inventory/
│   └── hosts.ini
├── playbooks/
│   ├── ping.yml
│   ├── httpd.yml
│   └── webcontent.yml
├── docs/
│   └── lab-environment.md
└── .gitignore
```

## Prerequisites

- Ansible Core installed on the control node
- SSH connectivity from `cnode` to each managed node
- A remote account with sudo/become privileges
- Python available on managed nodes
- Hostnames resolvable from the control node

## Configure and test

1. Edit `inventory/hosts.ini` and replace `YOUR_ADMIN_USER` with your managed-node SSH account.
2. Ensure `mac1` and `mac2` resolve through DNS or `/etc/hosts`.
3. Verify SSH access, then run:

```bash
ansible all -m ping
ansible-playbook playbooks/ping.yml
```

## Included playbooks

| Playbook | Purpose | Run |
|---|---|---|
| `ping.yml` | Verify Ansible connectivity | `ansible-playbook playbooks/ping.yml` |
| `httpd.yml` | Install, start and enable Apache on dev/test | `ansible-playbook playbooks/httpd.yml` |
| `webcontent.yml` | Create `/webdev` on dev with group ownership and SGID | `ansible-playbook playbooks/webcontent.yml` |

The web content directory uses mode `2775`: owner/group have read, write and execute; others have read and execute; SGID makes new contents inherit the directory group.

## Validate

```bash
ansible dev -m command -a "stat -c '%A %a %U:%G %n' /webdev"
ansible all -m command -a "systemctl is-enabled httpd"
```

## Security

- Never commit Vault passwords, private keys, tokens or production credentials.
- Keep local Vault password files out of Git.
- Use Ansible Vault for sensitive variables.
- Review target groups and privilege escalation before executing playbooks.

## Roadmap

- [ ] Add reusable roles
- [ ] Add templates and handlers
- [ ] Add encrypted group variables using Ansible Vault
- [ ] Add linting and syntax checks
- [ ] Add CI validation
- [ ] Document each lab with sanitized terminal output and screenshots

## Author

**Shaik Aiyaz** · Linux & Infrastructure Engineer  
[GitHub](https://github.com/shaikaiyazz) · [LinkedIn](https://www.linkedin.com/in/shaikaiyaz)

*Build Reliable Systems · Automate Workflows · Drive Innovation*
