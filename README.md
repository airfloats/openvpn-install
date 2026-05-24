**New: [wireguard-install](https://github.com/Nyr/wireguard-install) is also available.**

## openvpn-install
OpenVPN [road warrior](http://en.wikipedia.org/wiki/Road_warrior_%28computing%29) installer for Ubuntu, Debian, AlmaLinux, Rocky Linux, CentOS and Fedora.

This script will let you set up your own VPN server in no more than a minute, even if you haven't used OpenVPN before. It has been designed to be as unobtrusive and universal as possible.

# OpenVPN Install (Modified)

Fork from [Nyr/openvpn-install](https://github.com/Nyr/openvpn-install)

## Quick Start

```bash
wget https://raw.githubusercontent.com/airfloats/openvpn-install/master/openvpn-install.sh -O openvpn-install.sh && bash openvpn-install.sh
```

## Modifications

Based on the original script, the following changes have been made:

### Dual-Protocol Mode (TCP 443 + UDP 443)

- Simultaneously deploys two OpenVPN instances:
  - **TCP 443** — `tun0`, subnet `10.8.0.0/24`
  - **UDP 443** — `tun1`, subnet `10.8.1.0/24`
- Generates two client config files per user: `<client>-tcp443.ovpn` and `<client>-udp443.ovpn`
- Port 443 helps bypass restrictive firewalls that only allow HTTPS traffic

### IPv6 Disabled

- Removed all IPv6-related OpenVPN server configuration
- Automatically disables IPv6 system-wide on install via sysctl:
  ```
  net.ipv6.conf.all.disable_ipv6=1
  net.ipv6.conf.default.disable_ipv6=1
  net.ipv6.conf.lo.disable_ipv6=1
  ```
- Settings persist across reboots (`/etc/sysctl.d/99-openvpn-forward.conf`)

## Features Retained

- Supported OS: Ubuntu 22.04+, Debian 11+, AlmaLinux/Rocky/CentOS 9+, Fedora
- Add/revoke clients
- Full uninstall option
- Firewalld and iptables support
- SELinux compatibility
