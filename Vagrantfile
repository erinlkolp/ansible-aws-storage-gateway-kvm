# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "bento/rockylinux-9"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  
  config.vm.disk :disk, size: "256GB", primary: true

  config.vm.provider :virtualbox do |v|
    v.name = "kvmhost"
    v.memory = 16384
    v.cpus = 4
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.hostname = "kvmhost"
  config.vm.network :private_network, ip: "192.168.56.25"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :kvmhost do |kvmhost|
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "provisioning/sgw_preloader.yml"
    ansible.inventory_path = "provisioning/inventory"
    ansible.become = true
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "provisioning/sgw_deployer.yml"
    ansible.inventory_path = "provisioning/inventory"
    ansible.become = true
  end
end
