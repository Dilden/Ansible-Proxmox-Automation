# Dilden's Ansible + Proxmox Homelab Automation

## Installation
clone this repo

## Usage
/group_vars/virtualizer/creds.yml will need to be created via `ansible-vault create` and will need to be configured like so:
`---
vault_api_password: 'PROXMOX_HOST_PASSWORD'
`
From there, containers are configured within group_vars/virtualizer/vars.yml

After setting up everything, run the prep-host.yml playbook to ensure proxmoxer and other various dependencies are installed on the host.
