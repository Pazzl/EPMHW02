# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
  { hostname: 'vagrant-box-01', box: 'ubuntu/xenial64', ip: '192.168.15.2', ram: 1024 },
  { hostname: 'vagrant-box-02', box: 'ubuntu/xenial64', ip: '192.168.15.3', ram: 1024 }
]

Vagrant.configure("2") do |config|
	config.vm.synced_folder ".", "/vagrant", disabled: true

  nodes.each do |node|

    config.vm.define node[:hostname] do |node_config|
			node_config.vm.usable_port_range = (2200..2250)
      node_config.vm.hostname = node[:hostname]
      node_config.vm.box = node[:box]
			#As we have DHCP server at our bridged interface, we skip ip config
			node_config.vm.network "public_network", bridge: 'Qualcomm Atheros AR9285 Wireless Network Adapter'
			node_config.vm.network "private_network", ip: node[:ip], virtualbox__intnet: "intnet"
			
			node_config.vm.provider :virtualbox do |vb|
				vb.customize ["modifyvm", :id, "--memory", node[:ram]]
				vb.name = node[:hostname]
			end

    end
  end

end