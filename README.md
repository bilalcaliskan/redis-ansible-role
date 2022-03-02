# Redis Ansible Role
[![CI](https://github.com/bilalcaliskan/redis-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/redis-ansible-role/actions?query=workflow%3ACI)
[![GitHub tag](https://img.shields.io/github/tag/bilalcaliskan/redis-ansible-role.svg)](https://GitHub.com/bilalcaliskan/redis-ansible-role/tags/)

Installs and configures Redis servers as cluster or sentinel on Redhat/Debian based hosts.

## Requirements
This role has below requirements:
- [Python 3.x](https://www.python.org/downloads/)
- [Ansible](https://docs.ansible.com/) (min 2.4, suggested 2.9.16)

You can install suggested version with pip3:
```
$ pip3 install "ansible==2.9.16"
```

> Note that this role requires root access, so either run it in a playbook with a global `become: true`, or invoke the role in your playbook.

## Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role can ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to start and enable `firewalld` service, please modify below variable as true while running playbook:
> ```yaml
> firewalld_enabled: true
> ```


## Dependencies
This role depends on [bilalcaliskan.remi](https://galaxy.ansible.com/bilalcaliskan/remi) role on Redhat based hosts.

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

After you install all the tools above, you can simply configure [pre-commit](https://pre-commit.com/) by typing:
```shell
$ pre-commit install
```
## License
Apache License 2.0
