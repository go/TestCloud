# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos65"
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65"

  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "private_network", ip: "192.168.56.10"

  config.vm.provider "virtualbox" do |vb|
    at_disk = 'tmp/export.vdi'
    unless File.exists?(at_disk)
      vb.customize ['createhd', '--filename', at_disk, '--size', 10 * 1024]
    end
    vb.customize ['storageattach', :id, '--storagectl', 'SATA', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', at_disk]
  end

  config.vm.provision :ansible do |ansible|
    ansible.limit = "all"
    ansible.playbook = "playbook.yml"
    ansible.inventory_path = "hosts"
  end
end
