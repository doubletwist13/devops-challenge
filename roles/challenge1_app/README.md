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
```


- Required vars
  - backend_app_port - (scope: app servers ) - used to set the app listen port

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
