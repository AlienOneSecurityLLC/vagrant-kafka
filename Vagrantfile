# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  config.vm.box = "puppetlabs/centos-6.6-64-puppet"
  config.ssh.forward_agent = true # So that boxes don't have to setup key-less ssh
  config.ssh.insert_key = false # To generate a new ssh key and don't use the default Vagrant one
  config.vm.provision "shell", path: "scripts/init.sh", privileged: true
  
  # configure zookeeper cluster
  (1..3).each do |i|
    config.vm.define "zkafka#{i}" do |s|
      s.vm.hostname = "zkafka#{i}"
      s.vm.network "private_network", ip: "10.30.3.#{i+1}", netmask: "255.255.255.0", virtualbox__intnet: "my-network", drop_nat_interface_default_route: true
      #s.vm.provision "shell", path: "scripts/zookeeper.sh", args:"#{i}", privileged: false
    end
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
  end
end

