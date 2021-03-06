sonarqube-host
==============

Sonarqube-host is a role through which you are able to install and run Sonarqube with postgresql at the back-end. The web component is accessible through nginx rev-proxy with TLS set on. This role is designed to work on CentOS Stream 8, Fedora 34 server and Fedora 34 cloud image. Although, it can be easily customized to run on Debian/Ubuntu.

Dependencies
------------

For setting up Postgresql, you need to install community.postgresql with `ansible-galaxy collection install community.postgresql`

Requirements
------------

Sonarqube secrets are defined through hostvars in the Ansible inventory file (usually at `~/.ansible/inventory`).

Role Variables
--------------

All vars are defined in the `defaults/main.yml`

Example Playbook
----------------

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
