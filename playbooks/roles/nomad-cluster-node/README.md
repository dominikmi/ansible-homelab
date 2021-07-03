nomad-cluster-node
==================

Main goal is to automate Hashicorp Nomad cluster deployment with consul as service mesh and intergration with vault. So virtually, the nomad role consists of three deployments - Nomad, Consul and Vault. 

Requirements
------------

For now, it's written distinguishably for either Ubuntu 20.04 LTS or CentOS/Fedora.

Role Variables
--------------

There are just a couple of variables for this role now. All of them are used to render proper config file on each node.

- `nomad_server`: <IP_of_your_nomad_server>
- `nomad_data_dir`: </path/to/your/nomad/data>
- `consul_server`: <IP_of_your_consul_server>

This variable was moved into `inventory` file where I control the cluster's setup (which lab hosts are control plane (servers/both) and which become just clients):
- `nomad_node`: client|server|both  

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
