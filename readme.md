# Dilden's Ansible + Proxmox Homelab Automation

## What is this?
This repo contains the Ansible playbooks and configuration used to manage and automate my Proxmox based homelab.

## Installation
[Clone this repo](https://github.com/Dilden/Ansible-Proxmox-Automation)
Ensure you also have [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html) installed

## The main points
* Configuration is set in `ansible.cfg`. This exists only to tell Ansible where to look for server definitions (inventory).
* Servers (inventory) are defined in the `hosts` file and are placed in "groups" defined by `[]`
* The `group_vars` folder contains variables and credentials for use with the servers in those groups.
* `creds.yml` will need to be created via `ansible-vault create` in the appropriate folder and will need to be configured like so:
`---
vault_api_password: 'PROXMOX_HOST_PASSWORD'
`
From there, containers are configured within group_vars/virtualizer/vars.yml

After setting up everything, run the prep-host.yml playbook to ensure proxmoxer and other various dependencies are installed on the host.

## Usage
* Note: All commands will need to be run with `--ask-vault-pass` appended to them to work with this config. They no longer need to have `-u root` specified as that variable has been specified in the hosts.

Since I keep forgetting how to run these update commands, I figured I should document them here.

Update host: `ansible-playbook books/update-host-all.yml --ask-vault-pass -u root`
Update containers: `ansible-playbook books/update-containers.yml --ask-vault-pass -u root`

Some useful ad-hoc commands might look like:
`ansible closingtags -a "find /var/www/html/. -type f -mtime -15" --ask-vault-pass -u root` to find any files modified in the past 15 days

or `ansible closingtags -a "grep -nr 'atob' /var/www/html/." --ask-vault-pass -u root` to search all files for 'atob'.
