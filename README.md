Stouts.pull
===========

[![Build Status](https://travis-ci.org/Stouts/Stouts.pull.png)](https://travis-ci.org/Stouts/Stouts.pull)

Ansible role which manage [ansible-pull](http://docs.ansible.com/playbooks_intro.html#ansible-pull)

* Install and configure ansible-pull
* Setup SSH hosts and keys
* Setup cron task
* Setup logs


#### Variables

```yaml
pull_enabled: yes                       # The role is enabled

pull_ansible_ppa: ppa:rquillo/ansible   # Ansible ppa repository
pull_schedule: '*/15 * * * *'           # ansible-pull schedule
pull_user: "{{ansible_ssh_user}}"       # ansuble-pull user
pull_base_directory: /etc/ansible/local # ansible-pull setup directory
pull_logs_directory: "{{pull_base_directory}}/logs"
pull_work_directory: "{{pull_base_directory}}/work"

# Repository params
pull_repo_url: ""
pull_repo_version: "HEAD"
pull_only_if_changed: no
pull_playbook: ""
pull_inventory: ""
pull_verbose: vv

pull_know_hosts_file: ~{{pull_user}}/.ssh/known_hosts
pull_fingerprints:
   - "bitbucket.org,131.103.20.167 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAubiN81eDcafrgMeLzaFPsw2kNvEcqTKl/VqLat/MaB33pZy0y3rJZtnqwR2qOOvbwKZYKiEO1O6VqNEBxKvJJelCq0dTXWT5pbO2gDXC6h6QDXCaHo6pOHGPUy+YBaGQRGuSusMEASYiWunYN0vCAI8QaXnWMXNMdFP3jHAJH0eDsoiGnLPBlBp4TNm6rYI74nMzgz3B9IikW4WVK+dc8KZJZWYjAuORU3jc1c/NPskD2ASinf8v3xnfXeukU0sJ5N6m5E8VLjObPEO+mN2t/FZTMZLiFqPWc/ALSqnMnnhwrNi2rbfg/rd/IpL8Le3pSBne8+seeFVBoGqzHM9yXw=="
   - "github.com,204.232.175.90 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ=="

pull_private_key_path: ""
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

```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.pull/issues)!

