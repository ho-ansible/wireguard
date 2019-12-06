# Ansible role: WireGuard
Point-to-point VPN.

This role uses the built-in wireguard support in systemd-networkd as of v237.

Keys are stored as hostvars in YAML files in the inventory, and also cached as host facts.

## Requirements
Only tested on Debian stable, for now.
OpenVZ support is a to-do item.

## Role Variables
+ `wg_name` (default: `wg0`): name for the interface
+ `wg_ip` (default: `192.168.1.1/24`): IPv4 address and subnet of this host within the VPN
+ `wg_peers` (default: none): inventory host list
+ `wg_port` (default: empty): UDP port to use.  Set to empty to use the standard port 51820.
  + (This logic is used so that peers can look up the port in host vars.)
+ `wg_ext_ip` (default: `default`): public IPv4 address (without subnet).
  Peers will connect to this IP and create a firewall rule allowing packets from this IP.
  Set to string `default` to use `ansible_default_ipv4.address`.
  Set to empty to disable this behavior.

Additional optional role vars:
+ `wg_server_opts`: dict of additional options for `[WireGuard]` section
+ `wg_client_opts`: dict of additional options for this host's
  `[WireGuardPeer]` section on other hosts' config
+ `wg_routes`: list of additional subnets this host can route
+ `wg_network_opts`: additional text for the systemd network file, in ini format

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
