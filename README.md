
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

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
