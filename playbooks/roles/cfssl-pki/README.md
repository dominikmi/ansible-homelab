cfssl-pki
=========

*cfssl-pki* - this role sets CloudFlare's cfssl binaries on a host, generates required configs for creating ca and intermediate-ca, and generates key & cert pem with a given (defined role [client|server|peer]). This role should be used for one host that is designated to store ca and intermediate. Other hosts to be supplied with newly generated certs are populated from there. Each host has its cert role defined as var in ansible inventory file. This role serves its purpose for setting up a home/lab environment based on self generated CA on internal-only defined domains.

Already accomplished steps this role performs:

1. Installs cfssl & cfssljson
2. Creates configs for ca & intermediate certs in `/opt/ssl/config`
3. Creates profiles config (defines certs properties and capabilities) for client, peer and server certs - (cfssl.json)
4. Generates CA and Intermediate CA (signed by the CA cert)
5. Generates server certificate for the given internal domain's FQDN (`ansible_fqdn`)
6. Generating peer/server/client certificates for the defined pool of hosts

**[ This role is not ready yet ]**

To Do
-----

7. Certs & keys distribution across the hosts,
8. Some tests,
9. Additional playbooks to create client certificates (PFX bundled) for given workstations (browser level) for authentication/authorization to access secured services,

Requirements
------------

For now, it's written distinguishably for either Ubuntu 20.04 LTS or CentOS/Fedora.

Role Variables
--------------

Most vars used to fill in templates are defined in role's `defaults` directory. There are quite a bunch of them, yet they are pretty self explanatory. `vars/main.yml` contains only FQDN of the ca storing host. To properly run the tasks logic for `all` hosts the following hostvars are set in the `inventory` file: 
* `ca_store` = false|true
* `cert_role` = peer|server|client

Example Playbook
----------------

```
---
- name: use cfssl-pki role playbook
  hosts: <your_ca_store_host>
  become: true

  roles:
    - role: cfssl-pki
```

License
-------

BSD

Author Information
------------------

Dominik Miklaszewski
