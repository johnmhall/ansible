# ansible
The purpose of this repository is to provide any of my published Ansible playbooks for reference. I've provided an explanation of each of them below. Please contact me with any questions.

## deploy-wireguard.yml
This is the playbook that I currently use to deploy WireGuard in my own environment. This playbook is intended to be used on CentOS 7 and is still a work in progress although it works properly as provided.

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
