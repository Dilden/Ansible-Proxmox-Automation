# Dilden's Ansible + Proxmox Homelab Automation

## What is this?
This repo contains the Ansible playbooks and configuration used to manage and automate my Proxmox based homelab. It makes use of the [proxmox](https://docs.ansible.com/ansible/latest/modules/proxmox_module.html) and [proxmox_kvm](https://docs.ansible.com/ansible/latest/modules/proxmox_kvm_module.html) modules.

## Requirements
* [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html)
* [python >= 2.7](https://www.python.org/downloads/)
* [proxmoxer](https://pypi.org/project/proxmoxer/)
* [requests](https://pypi.org/project/requests/)


## Installation
[Clone this repo](https://github.com/Dilden/Ansible-Proxmox-Automation)
Ensure you also have [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html) (and all other requirements) installed

## The main points
* Configuration is set in `ansible.cfg`. This exists only to tell Ansible where to look for server definitions (inventory).
* Servers (inventory) are defined in the `hosts` file and are placed in "groups" defined by `[]`
* The `group_vars` folder contains variables and credentials for use with the servers in those groups.
* `creds.yml` will need to be created via `ansible-vault create` in the appropriate folder and will need to be configured like so:
`---
vault_api_password: 'PROXMOX_HOST_PASSWORD'

vault_100: 'CONTAINER_PASSWORD'
vault_101: 'CONTAINER_PASSWORD'
.
.
.
`
~~Just as the virtualizer API key needs to be set in `group_vars/virtualizer/creds.yml`, the containers will need to have passwords configured within `group_vars/containers/creds.yml` matching the appropriate variables set in `group_vars/containers/vars.yml`.~~

After setting up everything, run `ansible-playbook books\prep-host.yml` to ensure proxmoxer and other various dependencies are installed on the host.

## Usage
* Note: All commands will need to be run with `--ask-vault-pass` appended to them to work with this config.

Update host: `ansible-playbook books/update-host-all.yml --ask-vault-pass`

Update containers: `ansible-playbook books/update-containers.yml --ask-vault-pass`

Some useful ad-hoc commands might look like:
`ansible closingtags -a "find /var/www/html/. -type f -mtime -15" --ask-vault-pass` to find any files modified in the past 15 days

or `ansible closingtags -a "grep -nr 'atob' /var/www/html/." --ask-vault-pass` to search all files for 'atob'.
