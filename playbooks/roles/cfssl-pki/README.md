cfssl-pki
=========

*cfssl-pki* - this role sets CloudFlare's cfssl binaries on a host, generates required configs for creating ca and intermediate-ca, and generates key & cert pem with a given (defined role [client|server|peer]). This role should be used for one host that is designated to store ca and intermediate. Other hosts to be supplied with newly generated certs are populated from there. This role serves its purpose for setting up a home/lab environment based on self generated CA on internal-only defined domains.

Already accomplished steps this role performs:

1. Installs cfssl & cfssljson
2. Creates configs for ca & intermediate certs in `/opt/ssl/config`
3. Creates profiles config (defines certs properties and capabilities) for client, peer and server certs - (cfssl.json)
4. Generates CA and Intermediate CA (signed by the CA cert)
5. Generates server certificate for the given internal domain's FQDN (`ansible_fqdn`)

**[ This role is not ready yet ]**

To Do
-----

1. Generating peer/server/client certificates for the defined pool of hosts,
2. Certs & keys distribution across the hosts,
3. Some tests,
4. Additional playbooks to create client certificates (PFX bundled) for given workstations (browser level) for authentication/authorization to access secured services,

Role Variables
--------------

All vars are defined in role's `defaults` directory. There are quite a bunch of them, yet they are pretty self explanatory.

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
