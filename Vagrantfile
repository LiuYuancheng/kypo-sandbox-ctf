# Generated by Cyber Sandbox Creator 3.0.0
# https://gitlab.ics.muni.cz/muni-kypo-csc/cyber-sandbox-creator
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

ansible_groups = {
  "hosts" => ["transaction", "server"], 
  "routers" => ["router"], 
  "ssh" => ["router", "transaction", "server"], 
  "winrm" => [], 
  "ansible" => ["router", "transaction", "server"], 
  "user-accessible" => ["transaction"]
}

Vagrant.configure("2") do |config|

  # Device(router): router
  config.vm.define "router" do |device|
    device.vm.hostname = "router"
    device.vm.box = "munikypo/debian-10"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.0.6.1",
      netmask: "255.255.255.0"
    device.vm.network "private_network",
      virtualbox__intnet: "internet-connection",
      ip: "100.100.100.1",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "router"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.galaxy_role_file = "provisioning/requirements.yml"
      ansible.galaxy_roles_path = "provisioning/roles"
      ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
      ansible.limit = "router"
    end
  end

  # Device(host): transaction
  config.vm.define "transaction" do |device|
    device.vm.hostname = "transaction"
    device.vm.box = "munikypo/kali"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.0.6.23",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "transaction"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.galaxy_role_file = "provisioning/requirements.yml"
      ansible.galaxy_roles_path = "provisioning/roles"
      ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
      ansible.limit = "transaction"
    end
  end

  # Device(host): server
  config.vm.define "server" do |device|
    device.vm.hostname = "server"
    device.vm.box = "munikypo/debian-10"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.0.6.20",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "server"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.galaxy_role_file = "provisioning/requirements.yml"
      ansible.galaxy_roles_path = "provisioning/roles"
      ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
      ansible.limit = "server"
    end
  end

end
