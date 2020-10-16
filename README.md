# Hashicorp Tools (WIP)

[![Galaxy Quality](https://img.shields.io/ansible/quality/XXXXXX?style=flat&logo=ansible)](https://galaxy.ansible.com/monolithprojects/hashicorp_tools)
[![Role version](https://img.shields.io/github/v/release/MonolithProjects/ansible-hashicorp_tools)](https://galaxy.ansible.com/monolithprojects/hashicorp_tools)
[![Role downloads](https://img.shields.io/ansible/role/d/XXXXXX)](https://galaxy.ansible.com/monolithprojects/hashicorp_tools)
[![GitHub Actions](https://github.com/MonolithProjects/ansible-hashicorp_tools/workflows/molecule%20test/badge.svg?branch=master)](https://github.com/MonolithProjects/ansible-hashicorp_tools/actions)
[![License](https://img.shields.io/github/license/MonolithProjects/ansible-hashicorp_tools)](https://github.com/MonolithProjects/ansible-hashicorp_tools/blob/master/LICENSE)

This Ansible Role will install/uninstall Hashicorp tools.

## Requirements

## Role Variables

This is a copy from `defaults/main.yml`

```yaml
---
# URL to hashicorp download page
hashicorp_url: https://releases.hashicorp.com

# Hashicorp tools and their versions you want
# Supported state values are: present, reinstall, absent 
hashicorp_tools:
  []
    # - name: boundary
    #   version: 0.1.0
    #   state: present
    # - name: consul
    #   version: 1.8.0
    #   state: present
    # - name: nomad
    #   version: 0.10.3
    #   state: present
    # - name: packer
    #   version: 1.6.3
    #   state: present
    # - name: terraform
    #   version: 0.13.0
    #   state: present
    # - name: vagrant
    #   version: 2.2.7
    #   state: present
    # - name: vault
    #   version: 1.3.4
    #   state: present
    # - name: waypoint
    #   version: 0.1.1
    #   state: present

# Installation directory
install_dir: /usr/local/bin/
```

## Example Playbook

In this example the Ansible role will deploy (or redeploy) the GitHub Actions runner service (latest available version) and register the runner for the GitHub repo.
Runner service will run under the same user as the Ansible is using for ssh connection (*ansible*).

```yaml
---
- name: GitHub Actions Runner
  hosts: all
  user: ansible
  become: yes
  vars:
    - github_account: github-access-user
    - github_repo: my_awesome_repo
  roles:
    - role: monolithprojects.hashicorp_tools
```

In this example the Ansible role will uninstall Hashicorp Boundary and Install the rest of the Hashicorp tools with specific versions.

```yaml
---
- name: Hashicorp tools
  hosts: all
  vars:
      hashicorp_tools:
        - name: boundary
          state: absent
        - name: consul
          version: 1.8.0
          state: present
        - name: nomad
          version: 0.10.3
          state: present
        - name: packer
          version: 1.6.3
          state: present
        - name: terraform
          version: 0.13.0
          state: present
        - name: vagrant
          version: 2.2.7
          state: present
        - name: vault
          version: 1.3.4
          state: present
        - name: waypoint
          version: 0.1.1
          state: present
  roles:
      name: monolithprojects.hashicorp_tools
```

## License

MIT

## Author Information

Created in 2020 by Michal Muransky
