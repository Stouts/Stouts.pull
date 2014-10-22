Stouts.pull
===========

[![Build Status](http://img.shields.io/travis/Stouts/Stouts.pull.svg?style=flat-square)](https://travis-ci.org/Stouts/Stouts.pull)
[![Galaxy](http://img.shields.io/badge/galaxy-Stouts.pull-blue.svg?style=flat-square)](https://galaxy.pull.com/list#/roles/908)
[![Tag](http://img.shields.io/github/tag/Stouts/Stouts.pull.svg?style=flat-square)]()

Ansible role which manage [ansible-pull](http://docs.ansible.com/playbooks_intro.html#ansible-pull)

The role allows to you easy setup automatic updates for your server with `ansible-pull`.

* Install and configure ansible-pull
* Setup SSH hosts and keys
* Setup cron task
* Setup logs


#### Variables

```yaml
pull_enabled: yes                       # The role is enabled

pull_ansible_ppa: ppa:rquillo/ansible   # Ansible ppa repository
pull_schedule: '*/15 * * * *'           # Schedule crontab
pull_user: "{{ansible_ssh_user}}"       # Run from user
pull_group: "{{pull_user}}"
pull_user_ssh_home: ~{{pull_user}}/.ssh
pull_base_directory: /etc/ansible/local # ansible-pull base directory
pull_logs_directory: "{{pull_base_directory}}/logs"
pull_work_directory: "{{pull_base_directory}}/work"
pull_extra_vars: {}                     # Extra variables for pulling
                                        # Ex. pull_extra_vars:
                                        #       version: 1.2

# Repository params
pull_repo_url: ""
pull_repo_version: "HEAD"
pull_only_if_changed: no
pull_playbook: ""
pull_inventory:                         # Inventory hosts (each line will be addded to inventory as is)
- "{{inventory_hostname}} ansible_ssh_host=127.0.0.1"
pull_verbose: v

pull_fingerprints:
   - "bitbucket.org,131.103.20.167 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAubiN81eDcafrgMeLzaFPsw2kNvEcqTKl/VqLat/MaB33pZy0y3rJZtnqwR2qOOvbwKZYKiEO1O6VqNEBxKvJJelCq0dTXWT5pbO2gDXC6h6QDXCaHo6pOHGPUy+YBaGQRGuSusMEASYiWunYN0vCAI8QaXnWMXNMdFP3jHAJH0eDsoiGnLPBlBp4TNm6rYI74nMzgz3B9IikW4WVK+dc8KZJZWYjAuORU3jc1c/NPskD2ASinf8v3xnfXeukU0sJ5N6m5E8VLjObPEO+mN2t/FZTMZLiFqPWc/ALSqnMnnhwrNi2rbfg/rd/IpL8Le3pSBne8+seeFVBoGqzHM9yXw=="
   - "github.com,204.232.175.90 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ=="

pull_private_key_path: ""

pull_mail_to: ""                        # Set to enable notifications about errors
```

#### Usage

Add `Stouts.pull` to your roles and set vars in your playbook file.

Example:

```yaml

- hosts: all

  roles:
    - Stouts.pull

  vars:
    pull_user: vagrant
    pull_schedule: "* * * * *"
    pull_repo_url: "https://github.com/Stouts/Django-application.git"
    pull_repo_version: develop
    pull_private_key_path: "{{inventory_dir}}/keys/deploy"
    pull_playbook: "deploy/playbook.yml"
    pull_inventory: "deploy/inventory.ini"
    pull_extra_vars:
      pull_private_key_path: "{{pull_work_directory}}/keys/deploy" # !! Inventory directory will be changed

```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.pull/issues)!

