## Redis Ansible Role

[![Build Status](https://travis-ci.org/bilalcaliskan/redis-ansible-role.svg?branch=master)](https://travis-ci.org/bilalcaliskan/redis-ansible-role)

Installs and configures Redis with Sentinel to provide high availability on RHEL/CentOS servers.

## Requirements

No special requirements; note that this role requires root access, so either run it in a
playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: all
      become: true
      roles:
        - role: bilalcaliskan.redis

## Role Variables

Example parameters are listed below. See defaults/main.yml for all:

        redis_version: 5.0.7
        redis_port: 6379
        sentinel_port: 16379
        slave_read_only: yes
        redis_log_level: verbose
        redis_log_file: /var/log/redis/redis.log
        sentinel_log_file: /var/log/redis/sentinel.log
        max_memory: 6gb
        max_memory_policy: volatile-ttl
        num_of_databases: 16
        stop_writes_on_bgsave_error: yes
        enable_rdbcompression: yes
        enable_rdbchecksum: yes
        enable_appendonly: no
        redis_data_dir: /var/lib/redis
        sentinel_data_dir: /tmp
        cluster_name: sample-cluster
        quorum: 1


## Dependencies

This role depends on bilalcaliskan.remi role, so it contains that dependency on meta/main.yml.

## Example Playbook

    - hosts: all
      become: true
      vars_files:
        - vars/main.yml
      roles:
        - role: bilalcaliskan.redis

*Override the parameters you need to change inside `vars/main.yml`*:

        redis_version: 5.0.7
        redis_host: 0.0.0.0
        redis_port: 6379
        sentinel_port: 16379
        slave_read_only: yes
        redis_log_level: verbose
        redis_log_file: /var/log/redis/redis.log
        sentinel_log_file: /var/log/redis/sentinel.log
        max_memory: 6gb
        max_memory_policy: volatile-ttl
        num_of_databases: 16
        stop_writes_on_bgsave_error: yes
        enable_rdbcompression: yes
        enable_rdbchecksum: yes
        enable_appendonly: no
        redis_data_dir: /var/lib/redis
        sentinel_data_dir: /tmp
        cluster_name: sample-cluster
        quorum: 1

## License

MIT / BSD
