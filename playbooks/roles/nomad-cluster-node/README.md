Role Name
=========

`nomad-cluster-node` Nomad cluster role. Main goal is to automate Nomad cluster nodes deployment. 

Requirements
------------

For now, it's written for Ubuntu 20.04 LTS.

Role Variables
--------------

There are just a couple of roles now.

- `nomad_server`: <IP_of_your_nomad_server>
- `nomad_data_dir`: </path/to/your/nomad/data>
- `nomad_node`: client|server|both
- `consul_server`: <IP_of_your_consul_server>

Dependencies
------------
Nothing beyond default ansible setup yet.


Example Playbook
----------------

```    
---
- name: use nomad-cluster-node role playbook
  hosts: <your lab hosts>
  user: <your ansible user>
  become: true

  roles:
    - role: nomad-cluster-node

  post_tasks:
    - name: install nomad config
      template:
        src: roles/nomad-cluster-node/templates/nomad.hcl.j2
        dest: "/etc/nomad.d/nomad.hcl"
      changed_when: true
      notify: restart_nomad
```

License
-------

BSD

Author Information
------------------

Dominik Miklaszewski, fotoadmin@fotodev.org
