# Vagrantfile

This is a Vagrantfile that allows to setup development environment using Ansible as provisioner.

## Getting started

To use the vagrant file, you will need to have done the following:

  1. Download and Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) or VMWare Fusion.
  2. Download and Install [Vagrant](https://www.vagrantup.com/downloads.html)
  3. Install [Ansible](http://docs.ansible.com/intro_installation.html)
  4. Open a shell prompt (Terminal app on a Mac) and cd into the folder containing the `Vagrantfile`
  5. Run the following command to install the necessary Ansible roles for this profile: `$ ansible-galaxy install -r roles --roles-path=provisioning/roles --force`
  6. Edit `provisioning/group_vars/all` file with your data.

Once all of that is done, you can simply type in `vagrant up` (or `vagrant up --provider vmware_fusion` for VMWare Fusion), and Vagrant will create a new VM, install the base box, and configure it.

Once the new VM is up and running (after `vagrant up` is complete and you're back at the command prompt), you can log into it via SSH if you'd like by typing in `vagrant ssh`. Otherwise, the next steps are below.

## Boxes

Base boxes were taken from [phusion/open-vagrant-boxes](https://github.com/phusion/open-vagrant-boxes)

## Provisioning

Before `vagrant up` make sure you have correct sudo-user password in `provisioning/ansible_host` file.
Also you can enter your name and email for git in `provisionsing/group_vars/all` file.

## Thanks

There are some playbooks that helped me to build this one:

* [PostgreSQL Playbook](https://github.com/Kami/ansible-postgresql)
* [Redis Playbook](https://github.com/ICTO/ansible-redis)
