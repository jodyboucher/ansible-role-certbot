# Ansible role: certbot

[![Build Status](https://travis-ci.org/jodyboucher/ansible-role-certbot.svg?branch=master)](https://travis-ci.org/jodyboucher/ansible-role-certbot)

An [Ansible](https://www.ansible.com/) role that installs the certbot client.

The role does not obtain or install certificates - it only installs the certbot client.  You are expected to obtain the certificates and install as appropriate to your needs.

This role in intended for servers running nginx.

This role is designed for and tested on the following OS distributions:

* Ubuntu 16.04 Xenial
* Ubuntu 18.04 Bionic

## Requirements

* Ubuntu 16.04 Xenial or Ubuntu 18.04 Bionic
* [Ansible](https://docs.ansible.com/ansible/intro_installation.html) >= 2.4 (makes use of new import_tasks module)
* nginx
* This role requires `root` access so be sure to enable privilege escalation:

```yml
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

```yml
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

```yml
---
- hosts: webservers
  become: true
  vars_files:
    - vars/main.yml
  roles:
    - { role: certbot }
```

Inside `vars/main.yml`:

```yml
---
certbot_auto_renew_hour: 1
certbot_auto_renew_minute: 20
```

## Installation

On the command-line:

```bash
ansible-galaxy install git+https://github.com/jodyboucher/ansible-role-certbot.git
```

or in a role file (requirements.yml):

```yml
- name: certbot
  src: https://github.com/jodyboucher/ansible-role-certbot
  version: master
```

## License

MIT

## Author Information

This role was created by [Jody Boucher](https://jodyboucher.com/).
