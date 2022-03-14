haproxy
=========

A role to install and configure haproxy.

Requirements
------------

 Required vars:
  - backend_group_name - (scope: proxy servers) so haproxy knows what servers to add to the list of backend servers.
  - backend_app_port - (scope: app servers) so haproxy knows what port the backend app is listening on

Role Variables
--------------

Default variables (see `defaults/main.yml`)
```
haproxy_package_name: haproxy
haproxy_service_name: haproxy
haproxy_frontend_http_port: '80'
haproxy_frontend_https_port: '443'
haproxy_backend_app_port: '8888'
```

Ideally `haproxy_backend_app_port` will be set in hostvars or groupvars to override the default. 

Variables used by the template from the proxy server(s)
```
## Vars for the haproxy servers/group
inventory_hostname    # Sets the front-end name for the haproxy server itself.
ansible_default_ipv4.address  # Sets the IP address for haproxy to listen on.
haproxy_frontend_http_port # Sets listen port for HTTP.
haproxy_frontend_https_port # Sets listen port for HTTP (NOT YET IMPLEMENTED).
```

Variables used by the template from the app server(s) based on `groups[backend_group_name]`
```
inventory_hostname # Used to set the name of the backend servers.
backend_app_port  # Used to set the app port for each back-end server.
ansible_default_ipv4.address  # Sets the IP address for each backend server haproxy forwards to. 
```

Dependencies
------------
NONE

Example Playbook
----------------

```
- hosts: haproxy_servers
  gather_facts: false
  tasks:
    - name: Configure haproxy
      include_role:
        name: haproxy
```

License
-------

MIT
