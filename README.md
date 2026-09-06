# ansible-automation-scripts

This repository represent a collection of independant Ansible automations for provisioning and configuration, including system setup, storage, containers, orchestration, and monitoring.

Each folder is a **self-contained automation**: its own playbook, inventory file, and README, run them independantly depending on what you need to provision.

---
## Contents

| Folder | Purpose |
|---|---|
| [linux-baseline](./linux-baseline) | Base Linux system configuration | 
| [data-partitioning](./data-partitioning) | Disk partitioning setup | 
| [docker](./docker) | Docker install & configuration | 
| [docker-swarm](./docker-swarm) | Docker Swarm setup | 
| [linstor](./linstor) | LINSTOR storage setup | 
| [packages-upgrade](./packages-upgrade) | System package upgrades | 
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
│
├── linux-baseline/
│   ├── install.yml
│   ├── inventory.ini
│   └── readme.md
│
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
├── docker-swarm/
│   ├── templates/
│   │   └── daemon.json.j2
│   ├── install-swarm.yml
│   ├── inventory.ini
│   └── readme.md
│
├── linstor/
│   ├── install.yml
│   ├── inventory.ini
│   └── readme.md
│
├── packages-upgrade/
│   ├── install.yml
│   ├── inventory.ini
│   └── readme.md
│
├── zabbix-agent/
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
cd docker
ansible-playbook -i inventory.ini install-docker.yml
```

```bash
cd zabbix-agent
ansible-playbook -i inventory.ini install.yml
```

## Run
\`\`\`bash
ansible-playbook -i inventory.ini install.yml
\`\`\`

---
## Notes on Secrets & Inventories

- `inventory.ini` files in this repo use **placeholder/example hosts** — replace with your own IPs/hostnames before running.
- No real credentials, SSH keys, or vault passwords are committed.

---
