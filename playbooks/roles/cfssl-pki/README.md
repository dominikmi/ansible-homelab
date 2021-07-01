Role Name
=========

*cfssl-pki* - this role sets CloudFlare's cfssl binaries on a host, generates required configs for creating ca and intermediate-ca and generates key & cert pem with a given (defined role [client|server|peer]). This role should be used for one host that is designated to store ca and intermediate. Other hosts to be supplied with newly generated certs are populated from there. This role serves its purpose for setting up a home/lab environment based on self generated CA.

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
