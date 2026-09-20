# Debian 13 Server Hardening

Designed for a Debian 13 SSH server behind a MikroTik port-forward.

## Contents

- SSH public-key authentication
- Disable SSH passwords
- Disable root SSH login
- Disable X11/agent/TCP forwarding
- SSH connection limits
- nftables default-deny inbound firewall
- fail2ban SSH jail
- unattended security updates
- Lynis installation

## Before running

1. Confirm SSH key login works.
2. Keep an existing SSH session open.
3. Review `inventory.ini`.
4. Adjust variables in `roles/hardening/defaults/main.yml` if needed.

## Run

```bash
ansible-playbook -i inventory.ini site.yml --check
ansible-playbook -i inventory.ini site.yml
```

## Verify

```bash
sudo sshd -T
sudo nft list ruleset
sudo fail2ban-client status sshd
sudo ss -lntup
sudo lynis audit system
```

WARNING: The nftables policy permits only SSH inbound (plus ICMP/ICMPv6 and established traffic). Add rules before deploying services such as HTTP/HTTPS.
