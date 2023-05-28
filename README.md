ansible-role-satellite_proxmox_compute_ressource
=========

This role installs the community foreman plugin [ForemanFogProxmox](https://github.com/theforeman/foreman_fog_proxmox) to provide [Proxmox](https://www.proxmox.com) as Compute Resource in a [Red Hat Satellite](https://www.redhat.com/en/technologies/management/satellite)


Role Variables
--------------

| variable                        | default                                 | required | description                                                                       |
| :------------------------------ | :-------------------------------------- | :------- | :-------------------------------------------------------------------------------- |
| `foreman_repo_base_url`         | `'https://yum.theforeman.org/plugins'`  | false    | base URL of the Foreman plugin repository                                         |
| `foreman_repo_name`             | `'foreman-community-plugins'`           | false    | name of the repository created on the Satellite host                              |
| `foreman_repo_file`             | `'{{ foreman_repo_name }}'`             | false    | file of the repository created on the Satellite host                              |
| `foreman_repo_description`      | `'Forman community plugins'`            | false    | description of the repository created on the Satellite host                       |
| `foreman_proxmox_package`       | `'rubygem-foreman_fog_proxmox'`         | false    | name of the package which provides the Proxmox compute resource                   |
| `foreman_protector_plugin_name` | `'foreman-protector'`                   | false    | name of the foreman-protector to disable during installation of above package     |
| `run_satellite_installer`       | `true`                                  | false    | whether to run the satellite-installer after installing the package               |

Dependencies
------------

This role depends on the role `redhat.satellite_operations.installer` (if you are a Red Hat subscriber) or the upstream version `theforeman.operations.installer`. Should you choose to run the `foreman/satellite-installer` (`run_satellite_installer: true`).
The role makes use of the [common variables](https://theforeman.github.io/foreman-ansible-modules/latest/README.html#common-role-variables) which are defined when using `redhat.satellite_operations` or `redhat.satellite`.

Used variables from those roles are:
- `satellite_server_url`
- `satellite_username`
- `satellite_password`
- `satellite_validate_certs`

Should you use the `theforeman.*` collections, simply re-assigning the variables could be done to make this role usable for Foreman deployments:
```
---
- hosts: 'all'
  vars:
    satellite_server_url: '{{ foreman_server_url }}'
    [..]
  roles:
    - name: 'ansible-role-satellite_proxmox_compute_ressource'

```

Example Playbook
----------------

```
---
- name: 'Install Proxmox compute resource on a Red Hat Satellite'
  hosts: 'all'
  gather_facts: false
  vars:
    foreman_repo_base_url: 'https://yum.theforeman.org/plugins'
    foreman_repo_name: 'foreman-community-plugins'
    foreman_repo_file: '{{ foreman_repo_name }}'
    foreman_repo_description: 'Forman community plugins'
    foreman_proxmox_package: 'rubygem-foreman_fog_proxmox'
    foreman_protector_plugin_name: 'foreman-protector'
  roles:
    - name: 'ansible-role-satellite_proxmox_compute_ressource'
```
License
-------

GPL-2.0-or-later
