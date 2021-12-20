[![Ansible Lint](https://github.com/dominikmi/ansible-homelab/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/dominikmi/ansible-homelab/actions/workflows/ansible-lint.yml)

## ansible homelab set

There's just a bunch of ansible playbooks and roles for setting up and maintaining a homelab. All host pools and neccessary hostvars should be defined in `~/.ansible/inventory` before you run any of these below. Also, to run a given playbook on a single vm, you should run it with limit `-l machine_name`.

Roles
-----

I am currently working on the following `roles`:

- `cfssl-pki` : Automated cfssl based initial setup of internal CA, intermediate and server/peer/client certs for my internal domain,
- `gitlab-vm`: Initial Gitlab-CE setup, (*works in progress*)
- `livirt-vm` : to quickly spin up a KVM vm (FC34 or CentOS Stream 8) with static IP and further customized settings,
- `nomad-cluster-node` : A Hashicorp Nomad cluster setup with Consul and Vault, initial configs provisioned, (*needs some refinements*)
- `sonarqube-host` : SonarQube with postgresql and nginx.

Playbooks
---------

* `cfssl-pki-role.yaml` - Provision a vm with a host certificate based on self-signed CA
* `gitlab-vm-role.yaml` -  Provision a vm with initial Gitlab-CE setup
* `install-nextdns.yaml` - Provision a vm with NextDNS setup
* `install-python-selinux-binds.yaml` - Make sure that a vm has neccessary python bindings if SELinux is in place
* `install-virtualization.yaml` - Provision a vm/host with a @virtualization package
* `nomad-cluster-role.yaml` - Provision a vm with initial Nomad/Consul/Vault setup
* `setup-sudouser.yaml` - Get your user account ready to work with Ansible
* `setup-sq-role.yaml` - Provision a Sonarqube instance using sonarqube-host role
* `setup-vm-role.yaml` - Spin up a KVM vm based on FC34 image
* `update-labhosts.yaml` - Update labhost vm pool
* `update-sbx.yaml` - Update sandbox vm pool
