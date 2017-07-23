# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "server" do |server|
    memory_var_name = "PHPSERV_MEMORY"
    ip_var_name = "PHPSERV_IP"

    server.vm.box = "debian/contrib-jessie64"
    server.vm.hostname = "server"
    server.vm.network "private_network", ip: ENV[ip_var_name] || "192.168.1.10"

    server.vm.provider "virtualbox" do |vb|
      vb.memory = ENV.has_key?(memory_var_name) ? Integer(ENV[memory_var_name]) : 512
      vb.cpus = 1
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end

    server.vm.provision :shell, :path => "provisioning/provisioner-installer/debian-jessie.sh"
    server.vm.provision :shell, :inline => "cd /vagrant/provisioning/ansible/ && sudo ansible-playbook vagrant.yml"
  end
end
