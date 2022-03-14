
DevOps Challenge
================

Per the requirements set forth:

### Desired Challenge Outcome
Fully automated sample application environment using Ansible, Terraform, Chef and/or pure code to provision, manage and eventually destroy a minimum two-tier sample application of the applicant’s choice.  The front-end URL/endpoint should be returned as an output and accessible once execution is complete.

### Challenge Requirements
- Solution submission must be shared via git repository link
- CentOS, Redhat Enterprise Linux (RHEL), Debian or Ubuntu should be used as the base operating system
- The solution may be containerized, however, this not required
- The solution must be designed in a reusable, production oriented manner
- Documentation (readme, etc) should be included for the submitted solution
- Original code by the applicant with all references, licenses or any forks properly acknowledged and used only where it is necessary or additional benefits are provided
- The applicant does NOT need to build the application components/artifacts 
- Text explanation on the applicant’s approach including a brief overview of the architecture and thought process towards the desired challenge outcome

Requirements
------------

- Proxmox hypervisor with a cloud-init enabled template
  -  The user on the controller can log in as root via ssh key
- Currently depends on static IPs defined in inventory for each host. Mainly due to some dhcp/dns issues in my home network.

Variables
--------------

See readme for each of the following roles for details on variables used by these playbooks.
- proxmox_vm
- haproxy
- challenge1_app

Dependencies
------------

The following roles are required:
- proxmox_vm
- haproxy
- challenge1_app

Playbooks
---------

The following commands are used.

To deploy the application:
```
ansible-playbook -b -i hosts playbooks/challenge1_app_deploy.yml
```

To decommission/destroy the VMs for this application when you're done.  
   FAILSAFE: If some truthy boolean value for `TOTALDESTRUCTION` is not set, the playbook will fail without deleting VMs.
```
ansible-playbook -b -i hosts playbooks/decomm_playbooks/challenge1_app_destroy.yml -e TOTALDESTRUCTION=yes
```

License
-------

MIT
