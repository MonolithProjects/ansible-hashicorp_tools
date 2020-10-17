# Hashicorp Tools - Ansible Role

[![Galaxy Quality](https://img.shields.io/ansible/quality/51325?style=flat&logo=ansible)](https://galaxy.ansible.com/monolithprojects/hashicorp_tools)
[![Role version](https://img.shields.io/github/v/release/MonolithProjects/ansible-hashicorp_tools)](https://galaxy.ansible.com/monolithprojects/hashicorp_tools)
[![Role downloads](https://img.shields.io/ansible/role/d/51325)](https://galaxy.ansible.com/monolithprojects/hashicorp_tools)
[![GitHub Actions](https://github.com/MonolithProjects/ansible-hashicorp_tools/workflows/molecule%20test/badge.svg?branch=master)](https://github.com/MonolithProjects/ansible-hashicorp_tools/actions)
[![License](https://img.shields.io/github/license/MonolithProjects/ansible-hashicorp_tools)](https://github.com/MonolithProjects/ansible-hashicorp_tools/blob/master/LICENSE)

This Ansible Role will install/upgrade/uninstall Hashicorp tools.
Ansible Role does not use deb or rpm packages but installs the binaries directly from https://releases.hashicorp.com to the system.

- [Baundary](https://www.boundaryproject.io/)
- [consul](https://www.consul.io/)
- [Nomad](https://www.nomadproject.io/)
- [Packer](https://www.packer.io/)
- [Terraform](https://www.terraform.io/)
- [Vagrant](https://www.vagrantup.com/)
- [Vault](https://www.vaultproject.io/)
- [Waypoint](https://www.waypointproject.io/)

## Requirements

- Since the binaries are distributed inside of a Zip file, the role will automatically install `unzip` if it's not already on the system.

- In case you install `vagrant`, the role will automatically install `fuse` or `libfuse2` (depending on the packiging tool you system is using)

* Weekly tested on (but will run on older releases just fine):
  * CentOS 8
  * Debian 10
  * Fedora 32
  * Ubuntu 20

## Role Variables

This is a copy from `defaults/main.yml`

```yaml
---
# URL to hashicorp download page
hashicorp_url: https://releases.hashicorp.com

# Hashicorp tools and release versions.
# Supported state values are: present, absent
hashicorp_tools:
  []
    # - name: boundary
    #   version: 0.1.0
    #   state: present
    # - name: consul
    #   version: 1.8.4
    #   state: present
    # - name: nomad
    #   version: 0.12.5
    #   state: present
    # - name: packer
    #   version: 1.6.4
    #   state: present
    # - name: terraform
    #   version: 0.13.4
    #   state: absent
    # - name: vagrant
    #   version: 2.2.10
    #   state: present
    # - name: vault
    #   version: 1.5.4
    #   state: absent
    # - name: waypoint
    #   version: 0.1.1
    #   state: present

# Installation directory
install_dir: /usr/local/bin/
```

## Example Playbook

In this example the Ansible role will uninstall Hashicorp Boundary and install (or upgrade) the rest of the Hashicorp tools to specific release versions.

```yaml
---
- name: Hashicorp tools
  hosts: all
  vars:
      hashicorp_tools:
        - name: boundary
          state: absent
        - name: consul
          version: 1.8.4
          state: present
        - name: nomad
          version: 0.12.5
          state: present
        - name: packer
          version: 1.6.4
          state: present
        - name: terraform
          version: 0.13.4
          state: absent
        - name: vagrant
          version: 2.2.10
          state: present
        - name: vault
          version: 1.5.4
          state: absent
        - name: waypoint
          version: 0.1.1
          state: present
  roles:
      name: monolithprojects.hashicorp_tools
```

## Contribution

You are more than welcome to [contribute](https://github.com/MonolithProjects/ansible-hashicorp_tools/blob/master/CONTRIBUTING.md) ! :)

## License

MIT

## Author Information

Created in 2020 by Michal Muransky
