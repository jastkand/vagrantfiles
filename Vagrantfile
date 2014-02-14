# encoding: utf-8

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "opscode_ubuntu-12.04_chef-11.4.4"
  config.vm.box_url = "https://opscode-vm-bento.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_chef-11.4.4.box"

  config.vm.synced_folder "~/Projects", "/code"

  [3000, 4000, 4567, 9292].each do |port|
    config.vm.network :forwarded_port, guest: port, host: port
  end

  timezone = 'Europe/Moscow'
  config.vm.provision :shell, :inline => "echo \"#{timezone}\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/ansible_host"
    ansible.sudo = true
    # ansible.verbose = 'vvvv'
  end
end
