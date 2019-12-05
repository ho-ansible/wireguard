# Ansible role: WireGuard
Point-to-point VPN.

This role uses the built-in wireguard support in systemd-networkd as of v237.

Keys are stored as hostvars in YAML files in the inventory, and also cached as host facts.

## Requirements
Only tested on Debian stable, for now.

## Role Variables
+ `wg_name` (default: `wg0`): name for the interface
+ `wg_port` (default: 51820): UDP port to listen on
+ `wg_address` (default: `{{ ansible_default_ipv4.address }}`):
  public hostname/IP by which others can reach this node
+ `wg_ip` (default: `192.168.1.1/24`): IPv4 address and subnet of this host within the VPN
+ `wg_peers` (default: none): inventory host list

Additional optional role vars:
+ `wg_server_opts`: dict of additional options for `[WireGuard]` section
+ `wg_client_opts`: dict of additional options for this host's
  `[WireGuardPeer]` section on other hosts' config
+ `wg_network_opts`: additional text for the systemd network file,
  e.g., additional routes

## Dependencies
+ ho-ansible.systemd-networkd

## Example Playbook

```
- hosts: all
  roles:
    - { role: ho-ansible.wireguard }
```

## License
MIT

## Author Information
+ Ansible role: Sean Ho, https://github.com/ho-ansible/
+ Wireguard: https://www.wireguard.com/
