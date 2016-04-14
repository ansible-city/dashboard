# Dashboard

Master: [![Build Status](https://travis-ci.org/ansible-city/dashboard.svg?branch=master)](https://travis-ci.org/ansible-city/dashboard)  
Develop: [![Build Status](https://travis-ci.org/ansible-city/dashboard.svg?branch=develop)](https://travis-ci.org/ansible-city/dashboard)

This role installs and configures HoborgLabs Dashboard.




## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your
ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```




## Installation and Dependencies

This role depends on the following roles:
* ansible-city.users_and_groups
* ansible-city.nginx
* ansible-city.php




## Tags

This role uses two tags: **build** and **configure**

* `build` - Installs dashboard and all its dependencies
* `configure` - configures dashboard.




## Examples

To simply add swap to your server:

```YAML
- name: Add swap memory to the server
  hosts: sandbox

  pre_tasks:
    - name: Update apt
      become: yes
      apt:
        cache_valid_time: 1800
        update_cache: yes
      tags:
        - build

  roles:
    - role: ansible-city.dashboard
```

Ensure only `static` folder symlink - You've decided to keep your version of
`index.php`.

```YAML
- name: Add swap memory to the server
  hosts: sandbox

  pre_tasks:
    - name: Update apt
      become: yes
      apt:
        cache_valid_time: 1800
        update_cache: yes
      tags:
        - build

  roles:
    - role: ansible-city.dashboard
      dashboard:
        resources:
          - htdocs/static
```
