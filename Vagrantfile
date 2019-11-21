# -*- mode: ruby -*-
# vi: set ft=ruby sw=2 st=2 et :

# Maintainer : Ana SCHNEIDER ing.anacs@gmail.com
# We will create 5 servers :
# s0.infra, s1.infra ... s4.infra
#
# Use debian buster for our servers
Vagrant.configure("2") do |config|
  config.vm.box = "debian/buster64"
  config.vm.box_check_update = false

  # Limit memory of our servers
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1200"
    vb.gui = false
  end

  # Create a  cache for APT
  # config.vm.synced_folder 'v-cache', '/var/cache/apt'
  # Create s0.infra with intranet (eth1) and internet (eth0)
  config.vm.define 's0.infra' do |machine|
    machine.vm.hostname = 's0.infra'
    machine.vm.network "private_network", ip: "192.168.50.200"
    machine.vm.network "private_network", ip: "10.0.0.10"
  end

  # Create our servers (1 to 4) with intranet and internet
  4.times do |idx|
    config.vm.define "s#{idx + 1}.infra" do |machine|
      machine.vm.hostname = "s#{idx + 1}.infra" 
      machine.vm.network "private_network", ip: "192.168.50.#{(idx + 1) * 10 + 10}"
      machine.vm.network "private_network", ip: "10.0.0.#{idx + 11}"
      if idx == 0 
        machine.vm.network "forwarded_port", guest: 80, host: 80
        machine.vm.network "forwarded_port", guest: 8080, host: 8080
      end
    end
  end

  config.vm.provision "shell", path: "provision.sh"
end


