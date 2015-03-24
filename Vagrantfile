Vagrant.configure(2) do |config|
  config.vm.box = 'phusion-open-ubuntu-14.04-amd64'
  config.vm.box_url = "https://oss-binaries.phusionpassenger.com/vagrant/boxes/latest/ubuntu-14.04-amd64-vbox.box"

  # You can download the box and load it from local source
  # box_path = File.expand_path File.join('../Documents/vmware_fusion.box')
  # config.vm.box_url = "file://#{box_path}"

  config.vm.provider :vmware_fusion do |v, override|
    box_path = File.expand_path File.join('../../Documents/vmware_fusion.box')
    override.vm.box_url = "file://#{box_path}"
    # override.vm.box_url = 'https://oss-binaries.phusionpassenger.com/vagrant/boxes/latest/ubuntu-14.04-amd64-vmwarefusion.box'

    v.gui = false
  end

  config.vm.provider :virtualbox do |v|
    v.memory = 2048
    v.cpus = 2
  end

  [3000, 3500, 4000, 4567, 8888, 9292, 35729].each do |port|
    config.vm.network :forwarded_port, guest: port, host: port
  end

  config.vm.synced_folder '~/Projects', '/home/vagrant/code'

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'provisioning/playbook.yml'
    ansible.inventory_path = 'provisioning/ansible_host'
    ansible.sudo = true
    ansible.limit = 'all'
    ansible.verbose = 'vvvv'
  end
end
