# node_exporter

Deploys Prometheus node_exporter to Rocky Linux servers as a systemd service.
Handles binary download, user creation, service configuration, and firewall
rules automatically.

## Requirements

- Rocky Linux 8 or 9
- Ansible 2.9+
- Target host must have internet access (to download binary from GitHub)

## Role Variables

| Variable | Default | Description |
| -------- | ------- | ----------- |
| node_exporter_version | 1.7.0 | node_exporter release version |
| node_exporter_user | node_exporter | System user to run the service |
| node_exporter_group | node_exporter | System group for the service |
| node_exporter_port | 9100 | Port node_exporter listens on |
| node_exporter_install_dir | /usr/local/bin | Binary installation directory |

## Example Playbook
```yaml
- name: Deploy node_exporter
  hosts: monitored_servers
  become: yes
  roles:
    - node_exporter
```

## Tested On

- Rocky Linux 9
- AWX (Ansible Automation Platform)

## License

MIT

## Author

proclaudio — DevOps Infrastructure Lab
