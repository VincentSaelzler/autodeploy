# Automated Deployment
Cut down on the number of loosely organized shell scripts and web GUI commands that need to be executed. Automatically generate VMs, and embed required files and credentials.

## Software Stack
- Ansible (Red Hat)
- cloud-init (Canonical)
- Proxmox

Ansible is the most widely used component.

Proxmox has good integration with cloud-init. I don't need to use the detailed coud-init configuration files. I instead provide base configuration through `qe` command parameters. This sets up networking and SSH access. Then Ansible is used for the rest.

## Quick Start
Ensure that the computer running Ansible has key-based SSH access to the hosts in the `virtsrv` group.
```sh
:~/src/autodeploy$
ansible-playbook dotvalup.yaml --tags ssh #copy private key
ansible-playbook dotvalup.yaml --tags dl #download disk image (large)
ansible-playbook dotvalup.yaml --tags up #create and configure VM
ansible-playbook dotvalup.yaml --tags go #start VM
ansible-playbook dotvalup.yaml --tags down #stop and destroy VM
```
These can be combined. For example, from nothing to fully running VM:
```sh
ansible-playbook dotvalup.yaml --tags ssh,dl,up,go
```

## References
https://wiki.archlinux.org/title/Arch_Linux_on_a_VPS  
https://gitlab.archlinux.org/archlinux/arch-boxes#qcow2-images  
https://pve.proxmox.com/wiki/Cloud-Init_Support (includes documentation on creating the VMs)