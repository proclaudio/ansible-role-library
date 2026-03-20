# linux_hardening

CIS Benchmark-aligned security hardening role for Rocky Linux servers.
Implements 12 CIS controls across SSH, auditd, kernel parameters, password
policy, and service hardening. Deployed via AWX in Project 4.

## Requirements

- Rocky Linux 8 or 9
- Ansible 2.9+
- ansible.posix collection

## Role Variables

| Variable | Default | Description |
| -------- | ------- | ----------- |
| ssh_permit_root_login | no | CIS 5.2.8 - Disable root SSH |
| ssh_password_authentication | no | CIS 5.2.12 - Key auth only |
| ssh_client_alive_interval | 300 | CIS 5.2.13 - Idle timeout (seconds) |
| ssh_max_auth_tries | 3 | Maximum SSH authentication attempts |
| password_min_length | 14 | CIS 5.4.1 - Minimum password length |
| password_max_days | 90 | Maximum password age in days |
| auditd_max_log_file | 8 | Maximum audit log file size (MB) |

## CIS Controls Implemented

| Control | CIS Reference |
| ------- | ------------- |
| Disable root SSH login | CIS 5.2.8 |
| Enforce key authentication | CIS 5.2.12 |
| SSH idle timeout | CIS 5.2.13 |
| Enable auditd | CIS 4.1.1 |
| Audit login events | CIS 4.1.8 |
| Password minimum length | CIS 5.4.1 |
| Password complexity | CIS 5.4.1 |
| Restrict su command | CIS 5.6 |
| Disable IP forwarding | CIS 3.1.1 |
| Disable ICMP redirects | CIS 3.2.2 |
| Sticky bit on world-writable dirs | CIS 1.1.22 |
| Remove insecure services | CIS 2.3.4 |

## Safety Features

- SSH key check before disabling password auth (prevents lockout)
- sshd_config backed up before changes
- sshd -t validation before service restart
- Firewall check before applying rules

## Example Playbook
```yaml
- name: Harden servers
  hosts: target_servers
  become: yes
  roles:
    - linux_hardening
```

## Running Specific Controls
```bash
# SSH hardening only
ansible-playbook playbook.yml --tags ssh

# Kernel parameters only
ansible-playbook playbook.yml --tags kernel

# Audit configuration only
ansible-playbook playbook.yml --tags auditd
```

## Tested On

- Rocky Linux 9
- AWX (Ansible Automation Platform)

## License

MIT

## Author

proclaudio — DevOps Infrastructure Lab
