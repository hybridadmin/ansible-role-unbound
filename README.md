## Unbound Role

[![travis](https://travis-ci.com/hybridadmin/ansible-role-unbound.svg?branch=master)](https://travis-ci.com/hybridadmin/ansible-role-unbound.svg?branch=master) ![CI](https://github.com/hybridadmin/ansible-role-unbound/workflows/CI/badge.svg?branch=master) [![quality](https://img.shields.io/ansible/quality/49048)](https://galaxy.ansible.com/hybridadmin/unbound) [![downloads](https://img.shields.io/ansible/role/d/49048)](https://galaxy.ansible.com/hybridadmin/unbound)

> Install and configure unbound on your system with support for Plain DNS, DOT, DOH and Dnscrypt.

## Example Playbook

An example playbook can be specified as below:
```yaml
---
- hosts: all
  vars:
    unbound_version: 1.13.1
    unbound_temporary_directory: /tmp
    unbound_interface: 127.0.0.1
  roles:
    - role: hybridadmin.unbound
```

## Role Variables

The configuration options in [unbound.conf](https://nlnetlabs.nl/documentation/unbound/unbound.conf/) and what sections they should be used under are defined below:
```yaml
unbound_config: 
  server_section: 'options under the server: clause are defined here'
  remote_control_section: 'options under the remote-control: clause are defined here'
  stub_zone_section: 'options under the stub-zone: clause are defined here'
  forward_zone_section: 'options under the forward-zone: clause are defined here'
  auth_zone_section: 'options under the auth-zone: clause are defined here'
  view_section: 'options under the view: clause are defined here'
  python_section: 'options under the python: clause are defined here'
  dnscrypt_section: 'options under the dnscrypt: clause are defined here'
  rpz_section: 'options under the rpz: clause are defined here'
```

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for unbound

# What version to download/install.
unbound_version: 1.13.1

# Where to unpack unbound.
unbound_temporary_directory: /tmp

# The interface to listen on.
unbound_interface: 127.0.0.1

# configuration file settings
unbound_config:
  server_section:
    access-control: "0.0.0.0/0 allow"
    do-ip6: "no"
    chroot: ""
    aggressive-nsec: "yes"
    cache-max-ttl: 14400
    cache-min-ttl: 1200
    hide-identity: "yes"
    hide-version: "yes"
    prefetch: "yes"
    use-caps-for-id: "yes"
    verbosity: 1
    deny-any: "yes"
    log-queries: "yes"
    root-hints: "{{ unbound_config_dir }}/root.hints"
    trust-anchor-file: "{{ unbound_config_dir }}/root.key"
    num-threads: 4
    msg-cache-slabs: 4
    rrset-cache-slabs: 4
    infra-cache-slabs: 4
    key-cache-slabs: 4
    msg-cache-size: 256M
    rrset-cache-size: 512M
    outgoing-range: 8192
    num-queries-per-thread: 4096
    so-rcvbuf: 4m
    so-sndbuf: 4m
    ratelimit: 1000
    ratelimit-size: 1m
  remote_control_section:
    control-enable: "yes"  
```

## Requirements

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)


## License

Apache-2.0


## Author Information

hybridadmin
