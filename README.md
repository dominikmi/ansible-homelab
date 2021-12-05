## ansible homelab set

There's just a bunch of ansible playbooks and roles for setting up and maintaining a homelab.
I am currently working on the following roles:

- `cfssl-pki` : Automated cfssl based initial setup of internal CA, intermediate and server/peer/client certs for my internal domain,
- `gitlab-vm`: Initial Gitlab-CE setup (works in progress)
- `livirt-vm` : to quiclky spin up a KVM vm with static IP and further customized settings, 
- `nomad-cluster-node` : A Hashicorp Nomad cluster setup with Consul and Vault, initial configs provisioned/


