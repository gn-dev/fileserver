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
  end

  config.vm.define "scm" do |scm|
    scm.vm.hostname = "scm01"
    scm.vm.provider "virtualbox" do |vb|
      vb.name = "scm01"
      vb.memory = 1024
      vb.cpus = 1
    end
    scm.vm.network "private_network", ip: "192.168.7.3"
    scm.vm.network "forwarded_port", guest: 80, host: 8080
    # config.vm.network "public_network"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.sudo = true
    ansible.groups = {
      "fileservers" => ["fileservers"],
      "scm"         => ["scm"]
    }
  end
end
