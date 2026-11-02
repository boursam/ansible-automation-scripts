# Ansible Automation Scripts

A collection of independent Ansible playbooks for automating Linux infrastructure provisioning and configuration.

Each automation is self-contained, with its own playbook, inventory, templates (where required) and documentation. Automations can be executed independently depending on the configuration task.

## Automations

| Directory | Description |
|---|---|
| [`data-partitioning/`](./data-partitioning/) | Automated disk partitioning and storage configuration |
| [`docker/`](./docker/) | Docker installation and daemon configuration |
| [`zabbix-agent/`](./zabbix-agent/) | Zabbix Agent 2 installation and configuration |

Each directory contains a README with its specific requirements, variables and execution instructions.

## Repository Structure

```text
ansible-automation-scripts/
├── README.md
├── LICENSE
├── .gitignore
├── ansible.cfg
│
├── data-partitioning/
│   ├── config.yml
│   ├── inventory.ini
│   └── README.md
│
├── docker/
│   ├── templates/
│   │   └── daemon.json.j2
│   ├── install-docker.yml
│   ├── inventory.ini
│   └── README.md
│
└── zabbix-agent/
    ├── templates/
    │   └── zabbix-agent2.conf.j2
    ├── install-agent.yml
    ├── inventory.ini
    └── README.md
```

## Prerequisites

- Ansible installed on the control node.
- SSH connectivity to target hosts.
- Debian/Ubuntu-based target systems.
- A user with appropriate `sudo` privileges on target hosts.
- Inventory files configured with the target hosts and connection parameters.

## Usage

Navigate to the desired automation directory and execute its playbook.

**Docker installation**
```bash
cd docker
ansible-playbook -i inventory.ini install-docker.yml
```

**Zabbix Agent 2 installation**
```bash
cd zabbix-agent
ansible-playbook -i inventory.ini install-agent.yml
```

**Disk partitioning**
```bash
cd data-partitioning
ansible-playbook -i inventory.ini config.yml
```

For execution details and required variables, refer to the README inside each automation directory.

## Inventory and Credentials

- Inventory files contain example or placeholder hosts. Replace them with your target systems before execution.
- Do not commit production credentials, private SSH keys or Ansible Vault passwords.
- Use Ansible Vault or another secrets-management solution for sensitive variables.

## Notes

These playbooks are maintained as independent automations rather than a single end-to-end provisioning workflow.
