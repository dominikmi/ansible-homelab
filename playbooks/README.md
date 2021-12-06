An ansible driven homelab
=========================

An attempt to fully automate my homelab with Ansible. There's a bunch of playbooks and four roles creates so far. All pools and neccessary vars should be defined in `~/.ansible/inventory` before you run any of these below. Also, to run a given playbook on a single vm, I run it with limit `-l machine_name`.

* `cfssl-pki-role.yaml` - Provision a vm with a host certificate based on self-signed CA
* `gitlab-vm-role.yaml` -  Provision a vm with initial Gitlab-CE setup
* `install-nextdns.yaml` - Provision a vm with NextDNS setup
* `install-nginx.yaml` - Prosivion a vm with vanilla nginx 
* `install-python-selinux-binds.yaml` - Make sure that a vm has neccessary bindings if SELinux is in place
* `install-snap.yaml` - Provision a vm with snap if needed
* `install-virtualization.yaml` - Provision a vm/host with a @virtualization package
* `nomad-cluster-role.yaml` - Provision a vm with initial Nomad/Consul/Vault setup
* `setup-sudouser.yaml` - Get your user account ready to work with Ansible
* `setup-vm-role.yaml` - Spin up a KVM vm based on FC34 image
* `update-labhosts.yaml` - Update labhost vm pool
* `update-sbx.yaml` - Update sandbox vm pool

Happy ansibling 8-)