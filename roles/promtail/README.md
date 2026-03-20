# promtail

Deploys Grafana Promtail log shipping agent to Rocky Linux servers.
Configures Promtail to ship syslog, secure logs, and systemd journal
entries to a Loki endpoint. Handles binary download, user creation,
data directory, systemd service, and firewall rules automatically.

## Requirements

- Rocky Linux 8 or 9
- Ansible 2.9+
- Running Loki instance (see infrastructure-monitoring-stack)

## Role Variables

| Variable | Default | Description |
| -------- | ------- | ----------- |
| promtail_version | 2.9.4 | Promtail release version |
| promtail_user | promtail | System user to run the service |
| promtail_group | promtail | System group for the service |
| promtail_install_dir | /usr/local/bin | Binary installation directory |
| promtail_config_dir | /etc/promtail | Configuration directory |
| loki_url | http://192.168.111.40:3100 | Loki push endpoint |

## Log Streams Collected

| Stream | Source | Label |
| ------ | ------ | ----- |
| System messages | /var/log/messages | job=syslog |
| Security events | /var/log/secure | job=secure |
| Systemd journal | journald | job=systemd-journal |

## Example Playbook
```yaml
- name: Deploy Promtail
  hosts: log_sources
  become: yes
  vars:
    loki_url: "http://your-loki-server:3100"
  roles:
    - promtail
```

## Tested On

- Rocky Linux 9
- AWX (Ansible Automation Platform)

## License

MIT

## Author

proclaudio — DevOps Infrastructure Lab
