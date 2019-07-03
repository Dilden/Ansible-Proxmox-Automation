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
