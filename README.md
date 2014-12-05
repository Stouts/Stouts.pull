Stouts.pull
===========

[![Build Status](http://img.shields.io/travis/Stouts/Stouts.pull.svg?style=flat-square)](https://travis-ci.org/Stouts/Stouts.pull)
[![Galaxy](http://img.shields.io/badge/galaxy-Stouts.pull-blue.svg?style=flat-square)](https://galaxy.ansible.com/list#/roles/908)

Ansible role which manage [ansible-pull](http://docs.ansible.com/playbooks_intro.html#ansible-pull)

The role allows you to setup easily automatic updates for your server with `ansible-pull`.

* Install and configure ansible-pull;
* Setup SSH hosts and keys;
* Follow repositories and run ansible playbooks;
* Rotate logs;


#### Variables

```yaml
pull_enabled: yes                       # The role is enabled

pull_ansible_ppa: ppa:rquillo/ansible   # Ansible ppa repository

pull_user: "{{ansible_ssh_user}}"       # Run from user
pull_group: "{{pull_user}}"
pull_user_ssh_home: ~{{pull_user}}/.ssh

pull_prefix: /opt/ansible-pull          # Prefix directory
pull_logdir: "{{pull_prefix}}/var/log"  # Directory where logs will be stored
pull_workdir: "{{pull_prefix}}/etc/ansible-pull"   # Directory where jobs will be runned

pull_fingerprints:
- "bitbucket.org,131.103.20.167 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAubiN81eDcafrgMeLzaFPsw2kNvEcqTKl/VqLat/MaB33pZy0y3rJZtnqwR2qOOvbwKZYKiEO1O6VqNEBxKvJJelCq0dTXWT5pbO2gDXC6h6QDXCaHo6pOHGPUy+YBaGQRGuSusMEASYiWunYN0vCAI8QaXnWMXNMdFP3jHAJH0eDsoiGnLPBlBp4TNm6rYI74nMzgz3B9IikW4WVK+dc8KZJZWYjAuORU3jc1c/NPskD2ASinf8v3xnfXeukU0sJ5N6m5E8VLjObPEO+mN2t/FZTMZLiFqPWc/ALSqnMnnhwrNi2rbfg/rd/IpL8Le3pSBne8+seeFVBoGqzHM9yXw=="
- "github.com,204.232.175.90 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ=="

pull_private_keys: []                   # The keys will be copied to server
pull_schedule: '*/15 * * * *'           # Schedule crontab

pull_sources: []                        # Define your sources to control
                                        # Ex: pull_sources:
                                        #     - name: myproject
                                        #       repo: https://github.com/Stouts/Django-application.git
                                        #       version: develop
                                        #       playbook: deploy/playbook.yml
                                        #       vars:
                                        #         custom_var: value
# Default values
pull_playbook:                          # Set to related path to main playbook file
pull_extra_vars: {}                     # Extra variables for pull
                                        # Ex. pull_extra_vars:
                                        #       version: 1.2
pull_repo:
pull_version: "HEAD"
pull_only_if_changed: no
pull_inventory:                         # Inventory hosts (each line will be addded to inventory as is)
- "{{inventory_hostname}} ansible_ssh_host=127.0.0.1"
pull_verbose: v

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
    pull_schedule: "* * * * *"      # Cron schedule
    pull_private_keys:              # The key will be copied on server
    - "{{inventory_dir}}/keys/deploy"

    # Followed repositories
    pull_sources:
    - name: myproject
      repo: https://github.com/Stouts/Django-application.git
      version: develop
      playbook: deploy/playbook.yml
      vars:
        custom_var: value

```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.pull/issues)!
