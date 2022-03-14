challenge1_app
==============

A role to deploy and configure the challenge1 app

Requirements
------------

- Repos present to allow for install of `python3-flask` and `gunicorn`. Currently uses the default repos available in Debian buster.

Role Variables
--------------

Default variables (see `defaults/main.yml`)
```
challenge1_app_number_workers: 4
challenge1_app_appname: challenge1app
challenge1_app_service_user: challenge
challenge1_app_service_group: challenge
```

Additional variables used by templates
```
inventory_hostname
ansible_default_ipv4.address
backend_app_port 
```

Dependencies
------------

NONE


Example Playbook
----------------

```
- hosts: challenge1_app_servers
  gather_facts: true
  tasks:
    - name: Configure Challenge1 App VMs
      include_role:
        name: challenge1_app
```

License
-------

MIT
