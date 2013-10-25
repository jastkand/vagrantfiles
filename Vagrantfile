# encoding: utf-8

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "opscode_ubuntu-12.04_chef-11.4.4"
  config.vm.box_url = "https://opscode-vm-bento.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_chef-11.4.4.box"  

  config.vm.synced_folder "~/Projects", "/code"

  [3000, 4000, 4567, 9292].each do |port|
    config.vm.network :forwarded_port, guest: port, host: port, nfs: true
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks"]
    chef.add_recipe "apt"
    chef.add_recipe 'git'
    chef.add_recipe 'postgresql::server'
    chef.add_recipe 'postgresql::contrib'
    chef.add_recipe 'postgresql::server_dev'

    chef.add_recipe 'nodejs'
    chef.add_recipe 'nodejs::npm'

    chef.add_recipe 'ruby_build'
    chef.add_recipe 'rbenv::user'
    chef.add_recipe 'redis::install_from_package'
    chef.add_recipe 'oh_my_zsh'
    chef.add_recipe 'locale'
    chef.json = {
      'postgresql' => {
        "version" => "9.2",
        "users" => [
          {
            "username" => "vagrant",
            "password" => "password",
            "superuser" => true,
            "createdb" => true,
            "login" => true
          }
        ]
      },
      'rbenv' => {
        'user_installs' => [
          { 'user' => 'vagrant',
            'rubies' => ['2.0.0-p247'],
            'global' => '2.0.0-p247',
            'gems' => {
              '2.0.0-p247' => %w(bundler pg).collect{|gem_name| { 'name' => gem_name } }
            }
          }
        ]
      },
      'oh_my_zsh' => {
        'users' => [{
          :login => 'vagrant',
#          :theme => 'agnoster',
          :plugins => ['gem', 'git', 'redis-cli', 'ruby', 'heroku', 'rake', 'rbenv', 'capistrano']
        }]
      }
    }
  end
end
