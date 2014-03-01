# encoding: utf-8

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "vagrant-golang-box"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  config.vm.synced_folder "~/Projects", "/code"

  [3000, 4000, 4567, 9292].each do |port|
    config.vm.network :forwarded_port, guest: port, host: port
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/ansible_host"
    ansible.sudo = true
    ansible.verbose = 'vvvv'
  end
end
