# Ansible role: WireGuard
Point-to-point VPN.

This role uses the built-in wireguard support in systemd-networkd as of v237.

Keys are stored as hostvars in YAML files in the inventory, and also cached as host facts.

## Requirements
Debian bullseye.
Bare-metal or KVM, not container.

## Playbooks
+ `main.yml`: installs/configures wireguard
+ `uninstall.yml`: uninstalls wireguard. Run prior to removing host from inventory group.
+ `networks.yml`: multiple networks, configured from hostvars.

## Dependencies
+ [ho-ansible.systemd-networkd](https://github.com/ho-ansible/systemd-networkd)
+ [ho-ansible.systemd-resolved](https://github.com/ho-ansible/systemd-resolved)

## License
Ansible role licensed [MIT](LICENSE)

## Author Information
+ Ansible role by [Sean Ho](https://github.com/ho-ansible/)
+ [Wireguard](https://www.wireguard.com/)
