proxmox_vm
==========

Role to manage Proxmox VMs.  
Currently supports the following actions:

- Deploying new VMs from a cloud-init template
- Destroying existing VMs

Requirements
------------

- A proxmox instance
- A user in proxmox with permissions to perform any actions you are attempting
- (optional) An api key and token to use api keys for authentication
- community.general.proxmox_kvm module
- Requires the following python modules on the hypervisor:
  - proxmoxer
  - requests
  
Role Variables
--------------

Default variables (see `defaults/main.yml`)
Clones will default to use raw disks and linked clones
```
proxmox_vm_disk_type: raw     # Only used for full clones
proxmox_vm_full_clone: false
```

Variables required to specify the proxmox hypervisor and necessary credentials. Be sure to keep secrets encrypted in a vault or other secure source.
```
proxmox_api_host
proxmox_api_user
proxmox_api_password # If NOT using an api token auth
proxmox_api_token_id  # If using api token auth 
proxmox_api_token_secret # If using api token auth

```

Other required variables depending on what actions are being performed.
Other variables that might be needed depending on what actions are being performed.
```
proxmox_vm_template_name  # Required if cloning from a template
proxmox_vm_storage  # Reqruired if using full clones. Name of storage to be used for new VMs
vm_ip      # (scope: hostvars) Required to set static IP for any VM being created due to issue in my home network
inventory_hostname # (scope: magic_var) Used to set the name of the VM to be created/updated/destroyed
internal_net_gateway # (scope: groupvars) to set network gateway
internal_net_name # (scope: groupvars) to set DNS searchdomain for cloud-init enabled VMs
internal_net_dns # (scope: groupvars) to set DNS resolvers for cloud-init enabled VMs

```

Dependencies
------------

None

Example Playbook
----------------

Example playbook for deploying VMs.
```
---

- hosts: newvmhosts
  gather_facts: false
  
  # NOTE: Due to bug in proxmox_kvm and/or Proxmox API - MUST throttle to 1 at a time!
  tasks:
    - name: Deploy New VMs
      include_role:
        name: proxmox_vm
        apply:
          delegate_to: "{{ proxmox_api_host }}"
          throttle: 1
```

Example playbook for destroying VMs
```
- hosts: unneededvms
  gather_facts: false
  tasks:
    - name: Destroy VMs
      include_role:
        name: proxmox_vm
        tasks_from: destroy.yml
        apply:
          delegate_to: "{{ proxmox_api_host }}"

```

Caveats
-------

There are few things to be aware of with this role as it currently stands
- Due to a bug in proxmox_kvm and/or the proxmox api, if you don't throttle to 1 proxmox will try to deploy multiple VMs with the same VM ID. See https://github.com/doubletwist13/devops-challenge/issues/3
- Currently there are issues with timing as well. Until I learn the 'right' way to do it, there are some pauses added to prevent issues where it tries to configure VMs before the clone is finished, or tries to move on to other tasks before the VMs are up. See https://github.com/doubletwist13/devops-challenge/issues/2
- After cloning the VM, we use 'update' to set the static IP and network configuration. This is ACTING like it's not idempotent and thus shows as a change if you run again. I tried to get the static configuration in place during the initial clone action but it seems to ignore the settings.  See https://github.com/doubletwist13/devops-challenge/issues/22
  
License
-------

MIT
