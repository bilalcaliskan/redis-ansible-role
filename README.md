# Redis Ansible Role
[![CI](https://github.com/bilalcaliskan/redis-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/redis-ansible-role/actions?query=workflow%3ACI)
[![GitHub tag](https://img.shields.io/github/tag/bilalcaliskan/redis-ansible-role.svg)](https://GitHub.com/bilalcaliskan/redis-ansible-role/tags/)

Installs and configures Redis servers as cluster or sentinel on Redhat/Debian based hosts.

## Requirements
This role requires minimum Ansible version 2.4 and maximum Ansible version 2.9. You can install suggested version with pip:
```
$ pip install "ansible==2.9.16"
```

No special requirements; note that this role requires root access, so either run it in a
playbook with a global `become: true`, or invoke the role in your playbook.

## Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role will ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to stop and disable `firewalld` service, please modify below variable as false when running playbook:
> ```yaml
> firewalld_enabled: false


## Dependencies

This role depends on [bilalcaliskan.remi](https://galaxy.ansible.com/bilalcaliskan/remi) role on Redhat based hosts, so it contains that dependency on meta/main.yml.

## Examples

### Inventory
```
[redis]
node01.example.com
node02.example.com
node03.example.com
```

### Installation
**Standalone mode**
```yaml
- hosts: redis
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        install_redis: true
        sentinel_enabled: false
        cluster_enabled: false
```

**Sentinel mode**
```yaml
- hosts: redis
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        install_redis: true
        sentinel_enabled: true
        cluster_enabled: false
```

**Cluster mode**
```yaml
- hosts: redis
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        install_redis: true
        sentinel_enabled: false
        cluster_enabled: true
```

### Uninstallation
```yaml
- hosts: redis
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        install_redis: false
```

## Development
This project requires below tools while developing:
- [Ansible 2.4 or higher](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [pre-commit](https://pre-commit.com/)
- [ansible-lint](https://ansible-lint.readthedocs.io/en/latest/installing.html#using-pip-or-pipx) - required by [pre-commit](https://pre-commit.com/)
- [Bash shell](https://www.gnu.org/software/bash/) - required by [pre-commit](https://pre-commit.com/)

## License
Apache License 2.0
