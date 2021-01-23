# ansible
The purpose of this repository is to provide any of my published Ansible playbooks for reference. I've provided an explanation of each of them below. Please contact me with any questions. As I've just started converting my lab environments over to Debian 10, I've been adding new playbooks with -debian.yml as the extension that are still WIP.

## deploy-wireguard.yml
This is the playbook that I currently use to deploy WireGuard in my own environment. This playbook is intended to be used on CentOS 7 minimal and is still a work in progress although it works properly as provided.

This playbook makes use of the templates/wg0.conf.j2 file which should be updated with the appropriate values for your environment (yes, I'll turn these into variables at some point). This playbook also uses a vault to define all of the WireGuard peers. The vault entries should look like this:

```yaml
wgpeers:
  <name>:
    address: <ip>/32
    publickey: <key>
```

Here's an example of this block completed with a few peers:

```yaml
wgpeers:
  fredlaptop:
    address: 192.168.49.57/32
    publickey: UZqcNohm1G9nzT7mBhIknFzRgu01Gao07ga0oBPpQV0=
  fredphone:
    address: 192.168.49.58/32
    publickey: qdFmi8zVzFxGLcgpGfaqtaNoNohm1G9nz7Hx8PpQVF0=
  bethanyphone:
    address: 192.168.49.59/32
    publickey: Rgu01Gao07ga0oBPpQV0Rub4dFQ0VoLqNdLR9hlcWn4=
```

## deploy-kvm-host.yml
This is a playbook that I used to deploy the _majority_ of my KVM host in my lab. This playbook is intended to be used on CentOS 7 and is still a work in progress although it does work (but requires you to manually configure the br0 interface).

## deploy-newvm.yml
This is a playbook that I use to deploy CentOS 7 VMs on the system prepared with deploy-kvm-host.yml. This playbook is intended to be used with a CentOS 7 KVM host and is still a work in progress althouggh it does work properly as provided. This playbook requires an inventory file to be configured as demonstrated in the inventory/example.yml which contains the definitions of the VMs as well as various attributes. Here's the basic workflow you should follow:

1) Define your KVM host in the inventory along with all of the associated attributes that are shown in the example vs1 host.
2) Define the desired CentOS 7 image in the all>vars>images section as shown. This should be a link to the CentOS 7 Cloud Image at the appropriate level.
3) Define the properties of your VM underneath the host where it should be used. The examples guest1 and guest2 show how to properly define the VM and the associated attributes.
4) Execute the Playbook against the VM host to allocate the VM.

## deploy-new-host.yml
This is a playbook that I use to configure the Ansible user's permissions on a newly deployed system. This is only for use with newly-deployed bare-metal systems because I don't bother to maintain system images for these and just use the OS-provided installer. I do set the same default password for them initially and then go back and disable the ability to auth with password later.

## deploy-template.yml
This is a playbook used to deploy and configure my default template for a CentOS 7 system. This configures all of the typical settings that I would expect for a distributed system along with a set of useful tools used for troubleshooting in production environments.