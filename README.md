# ansible-automation-scripts

This repository represent a collection of independant Ansible automations for provisioning and configuration, including system setup, storage, containers, orchestration, and monitoring.

Each folder is a **self-contained automation**: its own playbook, inventory file, and README, run them independantly depending on what you need to provision.

---
## Contents

| Folder | Purpose |
|---|---|
| [data-partitioning](./data-patitionning) | Disk partitioning setup | 
| [docker](./docker) | Docker install & configuration | 
| [zabbix-agent](./zabbix-agent) | Zabbix agent install & configuration |

> Each subfolder has its own `readme.md` with specific run instructions, variables, and notes.
---

## Repository Structure
```
ansible-homelab/
├── README.md
├── LICENSE
├── .gitignore
├── ansible.cfg
|
├── data-partitioning/
│   ├── install.yml
│   ├── inventory.ini
│   └── readme.md
│
├── docker/
│   ├── templates/
│   │   └── daemon.json.j2
│   ├── install-docker.yml
│   ├── inventory.ini
│   └── readme.md
│
├── zabbix-agent/
    ├── templates/
    │   └── zabbix-agent2.conf.j2
    ├── install.yml
    ├── inventory.ini
    └── readme.md
```
---

## Pre-requisites
-   Ansibled installed/
-   SSH access configured to target hosts
-   Target hosts running a supported Linux distribution
-   `sudo` privilege escalation configured for the ansible user on targets
-   Debian/Ubuntu Distributions target

---

## Usage

Each automation is run idependently from its own folder:

```bash
cd zabbix-agent
ansible-playbook -i inventory.ini install.yml
```

---
## Notes on Secrets & Inventories

- `inventory.ini` files in this repo use **placeholder/example hosts** — replace with your own IPs/hostnames before running.
- No real credentials, SSH keys, or vault passwords are committed.

---
