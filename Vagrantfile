# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/jessie64"

  config.vm.define "fileservers" do |fileserver|
    fileserver.vm.hostname = "fs01"
    fileserver.vm.provider "virtualbox" do |vb|
      vb.name = "fs01"
      vb.memory = 512
      vb.cpus = 1
    end
    fileserver.vm.network "private_network", ip: "192.168.7.2"
    # config.vm.network "public_network"
    fileserver.vm.synced_folder "files", "/srv/files", type: "rsync"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.sudo = true
    ansible.groups = {
      "fileservers" => ["fileservers"],
    }
  end
end
