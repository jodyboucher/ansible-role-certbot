# Ansible role: certbot


An [Ansible](https://www.ansible.com/) role that installs the certbot client.

This role is designed for Ubuntu 16.04 Xenial.

## Requirements

This role requires `root` access so be sure to enable privilege escalation:

```
# privilege escalation of play
- hosts: webservers
  become: true
  roles:
    -role: certbot

# escalation of single role only
- hosts: webservers
  roles:
    - role: certbot
      become: true
```

## Role Variables

The available variables of this role are listed here along with default values:
```
# Set up a cron job to auto-renew the certificates.
# The job will run daily to determine if the certificates need to be renewed.
certbot_auto_renew: true

# The user for which the cron job is configured
certbot_auto_renew_user: "{{ ansible_user }}"

# The hour when the job should run
certbot_auto_renew_hour: 3

# The minute when the job should run
certbot_auto_renew_minute: 30

```

## Dependencies

None.

## Example Playbook

```
---
- hosts: webservers
  become: true
  vars_files:
    - vars/main.yml
  roles:
    - { role: certbot }
```

Inside `vars/main.yml`:

```
---
certbot_auto_renew_hour: 1
certbot_auto_renew_minute: 20
```

## Installation

On the command-line:
```
$ ansible-galaxy install git+https://github.com/jodyboucher/ansible-role-certbot.git
```

or in a role file (requirements.yml):

```
- name: certbot
  src: https://github.com/jodyboucher/ansible-role-certbot
  version: master
```

## License

MIT

## Author Information

This role was created by [Jody Boucher](https://jodyboucher.com/).
