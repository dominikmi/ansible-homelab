cfssl-pki
=========

*cfssl-pki* - this role sets CloudFlare's cfssl binaries on a designated host which will store CA and the Intermediate. It generates required configs for creating ca and intermediate-ca, and generates key & cert pem with a given (defined role [client|server|peer]). This role can be used with all hosts in your inventory, with the one designated to store ca and intermediate (flag: `ca_store` in hostvars). Other hosts to be supplied with newly generated certs are populated from there. Each host has its cert role defined as var in ansible inventory file. This role serves its purpose for setting up a home/lab environment based on self generated CA on internal-only defined domains.

Already accomplished steps this role performs:

1. Installs cfssl & cfssljson
2. Creates configs for ca & intermediate certs in `/opt/ssl/config`
3. Creates profiles config (defines certs properties and capabilities) for client, peer and server certs - (cfssl.json)
4. Generates CA and Intermediate CA (signed by the CA cert)
5. Generates server certificate for the ca storing host with given internal domain's FQDN (`ansible_fqdn`)
6. Generates peer/server/client certificates signed by the intermediate_ca, for the defined pool of hosts at `[all]` section in `inventory` file
7. Distributes the CA and Intermediate certs across all hosts.
8. Host certs & keys distribution across the hosts,


To Do
-----

9. Additional playbooks to create client certificates (PFX bundled) for given workstations (browser level) for authentication/authorization to access secured services,

Requirements
------------

For now, it's written distinguishably for either CentOS 8/Fedora 30+ or Ubuntu 20.04 LTS.

Role Variables
--------------

Most vars used to fill in templates are defined in role's `vars` directory. There are also OS specific variables useful when it comes to distribute the certs by a single task/handler. The `ca_store_host` is defined at `[all:vars]` in the `inventory` file. Additionally, to properly run the tasks logic for `all` hosts the following hostvars are set in the `inventory` file as well: 
* `ca_store` = false|true
* `cert_role` = peer|server|client

Example Playbook
----------------

To generate a host cert and provision vm with it:

```yaml
---
- name: use cfssl-pki role playbook
  hosts: <your_host>
  become: true

  roles:
    - role: cfssl-pki
```

To deploy whole setup, with hostvars: `ca_store` and cert roles (all hosts must be up):

```yaml
# Use for initial deployment across your lab hosts
- name: use cfssl-pki role playbook
  hosts: all
  become: true

  pre_tasks:
  - name: Gather facts from all hosts
    setup:
    delegate_to: "{{ item }}"
    delegate_facts: true
    when: hostvars[item]['ansible_fqdn'] is not defined
    with_items: "{{ groups['all'] }}"

  roles:
    - role: cfssl-pki
```

License
-------

BSD

Author Information
------------------

Dominik Miklaszewski
