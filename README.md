# Ansible role: WireGuard
Point-to-point VPN.

This role uses the built-in wireguard support in systemd-networkd as of v237.

Keys are stored as hostvars in YAML files in the inventory, and also cached as host facts.

## Requirements
Only tested on Debian stable, for now.
Installs backports kernel for in-tree wireguard module (no DKMS needed).
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
  Set to empty string disable this behavior.
+ `wg_routes`: list of additional subnets this host can route as gateway (`AllowedIPs`).
  Also affects routing in systemd network config.
  These routes will be added with high metric (hard-coded at 1024).

Optional role vars for `[Wireguard]` section of netdev:
+ `wg_fwmark`: firewall mark to set on outgoing packets

Optional role vars for `[WireguardPeer]` section of netdev:
+ `wg_psk`: preshared key generated by `wg genpsk`
+ `wg_keepalive`: interval in seconds to send keepalive packets.
  If this variable is set, the option will be enabled for all peers from this host.

Optional role vars for systemd network file:
+ `wg_dns`: list of DNS servers
+ `wg_domains`: list of domains using above DNS servers, optionally prefixed with `~`.
  See systemd.network(5).
+ `wg_network_opts`: additional text for the systemd network file, in ini format
  with newlines

Optional role vars for systemd-networkd service:
+ `wg_extra_iptables`: list of additional firewall rules, as strings starting with the chain name.

Optional role vars for installing wireguard:
+ `wg_repo` (default: `http://http.us.debian.org/debian/`): debian repository
+ `wg_repo_rel` (default: `bullseye`): release for above repo.
  This needs to be a name (buster, bullseye), rather than an alias (stable, testing).

## Playbooks
+ `main.yml`: installs/configures wireguard
+ `uninstall.yml`: uninstalls wireguard. Run before removing from inventory group.

## Dependencies
+ [ho-ansible.systemd-networkd](https://github.com/ho-ansible/systemd-networkd)
+ [ho-ansible.systemd-resolved](https://github.com/ho-ansible/systemd-resolved)

## License
Ansible role licensed [MIT](LICENSE)

## Author Information
+ Ansible role by [Sean Ho](https://github.com/ho-ansible/)
+ [Wireguard](https://www.wireguard.com/)
