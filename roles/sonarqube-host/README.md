Role Name
=========

Sonarqube-host is a role through which you are able to install and run Sonarqube with postgresql at the back-end. The web component is accessible through nginx rev-proxy with TLS set on. This role is designed to work on Fedora 34 server and Fedora 34 cloud image. Although, it can be easily customized to run on Debian/Ubuntu.

(WIP: pgsql, nginx and the TLS certs provisioning)

Requirements
------------

Sonarqube secrets are defined through hostvars at the Ansible inventory file.

Role Variables
--------------

All vars are defined in the `defaults/main.yml`

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: Deploy and run Sonarqube
  hosts: labhost
  gather_facts: true
  become: true
  tasks:
    - name: Sonarqube role
      include_role:
        name: sonarqube-host
```

License
-------

BSD

Author Information
------------------

Dominik Miklaszewski, 12.2021
