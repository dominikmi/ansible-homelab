libvirt-vm
==========

This role is intended to quickly bring up a local libvirt VM with assigned static IP within the pre-defined "default" network on the host in "NAT" mode. The base image is sourced from either a Fedora 34 Cloud or CentOS Stream 8 Cloud. If the `vm_ip` var is not passed the vm will be spun up with DHCP setup. This is an attempt to creatively extend a brilliantly simple solution published at: https://www.redhat.com/sysadmin/build-VM-fast-ansible

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

* `fc_base_image_name`: Fedora-Cloud-Base-34-1.2.x86_64.qcow2
* `fc_base_image_url`: https://download.fedoraproject.org/pub/fedora/linux/releases/34/Cloud/x86_64/images/{{ base_image_name }}
* `fc_base_image_sha`: b9b621b26725ba95442d9a56cbaa054784e0779a9522ec6eafff07c6e6f717ea
* `ce_base_image_name`: CentOS-Stream-GenericCloud-8-20210603.0.x86_64.qcow2
* `ce_base_image_url`: https://cloud.centos.org/centos/8-stream/x86_64/images/{{ ce_base_image_name }}
* `ce_base_image_sha`: 8e22e67687b81e38c7212fc30c47cb24cbc4935c0f2459ed139f498397d1e7cd
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
`ansible-playbook -K setup-vm-role.yaml -e "vm_name=myvmname user=myusername vm_ip=192.168.11.15 resize_vm=yes"`

The playbook:

```yaml
- name: Deploys VM based on a FC34 cloud image
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
