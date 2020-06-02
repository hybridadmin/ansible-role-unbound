# unbound

Install and configure unbound on your system.

|Travis|GitHub|Quality|Downloads|
|------|------|-------|---------|
|[![travis](https://travis-ci.org/hybridadmin/ansible-role-unbound.svg?branch=master)](https://travis-ci.org/hybridadmin/ansible-role-unbound.svg?branch=master)|[![github](https://github.com/hybridadmin/ansible-role-unbound/workflows/Ansible%20Molecule/badge.svg)](https://github.com/hybridadmin/ansible-role-unbound/actions)|[![quality](https://img.shields.io/ansible/quality/45335)](https://galaxy.ansible.com/hybridadmin/unbound)|[![downloads](https://img.shields.io/ansible/role/d/45335)](https://galaxy.ansible.com/hybridadmin/unbound)|

## Example Playbook

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: hybridadmin.unbound
```

For verification `molecule/resources/verify.yml` run after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    _nslookup_package:
      default:
        - bind-utils
      Debian:
        - dnsutils

    nslookup_package: "{{ _nslookup_package[ansible_os_family] | default(_nslookup_package['default']) }}"

  tasks:
    - name: install nslookup
      package:
        name: "{{ nslookup_package }}"
        state: present

    - name: nslookup google.com
      command: nslookup google.com
```

## Role Variables

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
  remote_control_section:
    control-enable: "yes"  
```

## Requirements

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

## Compatibility

This role has been tested on these [container images](https://hub.docker.com/):

|container|tags|
|---------|----|
|el|7, 8|
|ubuntu|18.04, 20.04|
|fedora|31, 32|
|opensuse|all|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

## Exceptions

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| alpine | Idempotence test failed: start and enable unbound |


## Testing

[Unit tests](https://travis-ci.com/hybridadmin/ansible-role-unbound) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/hybridadmin/ansible-role-unbound/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `hybridadmin`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `hybridadmin`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `hybridadmin`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## License

Apache-2.0


## Author Information
