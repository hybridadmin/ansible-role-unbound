# unbound

Install and configure unbound on your system.

|Travis|GitHub|Quality|Downloads|
|------|------|-------|---------|
|[![travis](https://travis-ci.org/hybridadmin/ansible-role-unbound.svg?branch=master)](https://travis-ci.org/hybridadmin/ansible-role-unbound.svg?branch=master)|[![github](https://github.com/hybridadmin/ansible-role-unbound/workflows/Ansible%20Molecule/badge.svg)](https://github.com/hybridadmin/ansible-role-unbound/actions)|[![quality](https://img.shields.io/ansible/quality/45335)](https://galaxy.ansible.com/hybridadmin/unbound)|[![downloads](https://img.shields.io/ansible/role/d/45335)](https://galaxy.ansible.com/hybridadmin/unbound)|

## Example Playbook

An example playbook can be specified as below:
```yaml
---
- hosts: all
  vars:
    unbound_version: 1.10.1
    unbound_temporary_directory: /tmp
    unbound_interface: 127.0.0.1
    unbound_port: 53
  roles:
    - role: hybridadmin.unbound
```

## Role Variables

The configuration options in [unbound.conf](https://nlnetlabs.nl/documentation/unbound/unbound.conf/) and what sections they should be used under and defined below:
```yaml
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
unbound_version: 1.10.1

# Where to unpack unbound.
unbound_temporary_directory: /tmp

# The interface to listen on.
unbound_interface: 127.0.0.1

# The port to listen on.
unbound_port: 53

# configuration file settings
unbound_settings:
  server_section:
    access-control: "0.0.0.0/0 allow"
    do-ip4: "yes"
    do-ip6: "no"
    do-udp: "yes"
    do-tcp: "yes"
    chroot: ""
    username: "unbound"
    aggressive-nsec: "yes"
    cache-max-ttl: 14400
    cache-min-ttl: 1200
    hide-identity: "yes"
    hide-version: "yes"
    interface: 0.0.0.0
    prefetch: "yes"
    rrset-roundrobin: "yes"
    use-caps-for-id: "yes"
    verbosity: 3
    deny-any: "yes"
    harden-glue: "yes"
    harden-dnssec-stripped: "yes"
    log-queries: "yes"
    root-hints: "/usr/local/etc/unbound/named.root"
    trust-anchor-file: "/usr/local/etc/unbound/root.key"
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
    so-reuseport: "yes"
    ratelimit: 1000
    ratelimit-size: 1m
  remote_control_section:
    control-enable: "yes"
    server-key-file: "/usr/local/etc/unbound/unbound_server.key"
    server-cert-file: "/usr/local/etc/unbound/unbound_server.pem"
    control-key-file: "/usr/local/etc/unbound/unbound_control.key"
    control-cert-file: "/usr/local/etc/unbound/unbound_control.pem"  
```

## Requirements

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)


## License

Apache-2.0


## Author Information

hybridadmin
