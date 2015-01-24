# Vagrantfile

This is a Vagrantfile that allows to setup development environment using Ansible as provisioner.

## Installation

```
$ gem install vagrant
```

[Install Ansible](http://docs.ansible.com/intro_installation.html)

```
$ vagrant up
```

## Provisioning

Before `vagrant up` make sure you have correct sudo-user password in `provisioning/ansible_host` file.
Also you can enter your name and email for git in `provisionsing/group_vars/all` file.

## Thanks

There are some playbooks that helped me to build this one:

* [PostgreSQL Playbook](https://github.com/Kami/ansible-postgresql)
* [Redis Playbook](https://github.com/ICTO/ansible-redis)
* [rbenv Playbook](https://github.com/leucos/ansible-rbenv-playbook)
