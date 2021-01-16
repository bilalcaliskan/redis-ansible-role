## Redis Ansible Role

[![CI](https://github.com/bilalcaliskan/redis-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/redis-ansible-role/actions?query=workflow%3ACI)

Installs and configures Redis with Sentinel to provide high availability on RHEL/CentOS servers.

### Requirements

No special requirements; note that this role requires root access, so either run it in a
playbook with a global `become: true`, or invoke the role in your playbook like:

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        simple_role_var: foo
```

### Role Variables

See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role will ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to stop and disable `firewalld` service, please modify below variable as false when running playbook:  
> ```yaml  
> firewalld_enabled: false


## Dependencies

This role depends on [bilalcaliskan.remi](https://galaxy.ansible.com/bilalcaliskan/remi) role, so it contains that dependency on meta/main.yml.

### Example Inventory File

```
[redis]
node01.example.com
node02.example.com
node03.example.com
```

### Example Playbook File For Installation With `Standalone Mode`
```yaml
- hosts: redis
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        redis_install: true
        sentinel_enabled: false
        cluster_enabled: false
```

### Example Playbook File For Installation With `Sentinel Mode`
```yaml
- hosts: redis
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        redis_install: true
        sentinel_enabled: true
        cluster_enabled: false
```

### Example Playbook File For Installation With `Cluster Mode`
```yaml
- hosts: redis
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        redis_install: true
        sentinel_enabled: false
        cluster_enabled: true
```

### Example Playbook File For `Uninstallation`

```yaml
- hosts: redis
  become: true
  roles:
    - role: bilalcaliskan.redis
      vars:
        redis_install: false
```

### License

MIT / BSD
