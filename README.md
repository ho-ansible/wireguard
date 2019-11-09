# Ansible role: WireGuard
Point-to-point VPN.

## Requirements
Only tested on Debian stable, for now.

## Role Variables
+ `wg_name` (default: `wg0`): name for the interface
+ `wg_port` (default: 51820): UDP port to listen on
+ `wg_host` (default: none): host/address by which others can reach this node
+ `wg_ip` (default: `192.168.1.1/24`): IPv4 address and subnet of this host within the VPN
+ `wg_peers` (default: none): inventory host list
+ `wg_privkey`: private key, use `wg genkey` to make a new one
+ `wg_pubkey`: public key, use `cat privkey | wg pubkey` to obtain
+ `wg_server_opts` (default: none): dict of additional options for `[WireGuard]` section
+ `wg_client_opts` (default: none): dict of additional options for this host's
  `[WireGuardPeer]` section on other hosts' config
+ `wg_network_opts` (default: empty): additional text for the systemd network file,
  e.g., additional routes

## Dependencies
None.

## Example Playbook

```
- hosts: all
  roles:
    - { role: ho-ansible.template }
```

## License
MIT

## Author Information
+ Ansible role: Sean Ho, https://github.com/ho-ansible/
+ Wireguard: https://www.wireguard.com/
