libvirt-vm
==========

This role is intended to quickly bring up a local libvirt VM with assigned static IP within the pre-defined "default" network on the host in "NAT" mode. The base image is sourced from either a Fedora 35 Cloud or CentOS Stream 9 Cloud (if you'd rather pick the previous 34 and 8 respectively, please go to default/main.yml and replace the existing values). If the `vm_ip` var is not passed the vm will be spun up with DHCP setup. This is an attempt to creatively extend a brilliantly simple solution published at: https://www.redhat.com/sysadmin/build-VM-fast-ansible

Additional features:
* Since the base FC34 image is only 5GB, I added optional extension of +10GB,
* Static IP setup within the "default" network is provisioned through a networking-script (`ifcfg-eth0`)
* No `vm_ip` set will result in DHCP IP
* The VM is provisioned with a user account and its public key from the host, 
* This user gets set up in `sudoers` for any further works with host's Ansible scripts

(Additional options to work on would be handling other cloud base images from CentOS or Ubuntu or choosing from different host virtual network definitions other than "default" one).

Requirements
------------

1. Already set up and working KVM on the localhost, with at least "default" network defined,
2. If you have a local DNS in place with local domain configured, define the names of the VMs within this domain. It will be useful when you want to further experiment with TLS based accessible solutions.

Role Variables
--------------

Default variables with default values (in role's `default`), used by the tasks:

[..]
* `vm_pool_dir`: "/var/lib/libvirt/images"
* `vm_name`: labvm
* `vm_vcpus`: 2
* `vm_ram_mb`: 2048
* `vm_net`: default
* `cleanup_tmp`: no
* `user_pub_ssh_key`: /home/{{ user }}/.ssh/id_rsa.pub
* `resize_vm`: no
* `vm_os`: fedora

These default values can be overriden by passing their new values with `-e` in the CLI. Especially the `vm-name` if you have your own local DNS in place.

Other variables passed through `-e`:
* `user`: <username_on_the_host_with_already_set_up_ssh_keys>
* `vm_ip`: <a_static_IP_within_your_libvirt_default_network>
* `vm_os`: fedora|centos

Dependencies
------------

* `community.libvirt.virt`

Templates
---------

There are currently two templates, which need to be customized to your own needs and host setup.

* `templates/sbx-template.xml.j2` - initial image configuration 
* `templates/ifcfg-eth0.j2` - Static IP based configuration for the VM 

Example Playbook
----------------

Example: run this role on your laptop, with KVM already installed, configured and running:
`ansible-playbook -K setup-vm-role.yaml -e "vm_os=centos vm_name=myvmname user=myusername vm_ip=192.168.11.15 resize_vm=yes"`

The playbook:

```yaml
- name: Deploys VM based on a FC34 or CenOS Stream 8 cloud image
  hosts: localhost
  gather_facts: yes
  become: yes
  tasks:
    - name: Libvirt VM role
      include_role:
        name: libvirt-vm
```

License
-------

BSD
