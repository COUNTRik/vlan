# -*- mode: ruby -*-
# vim: set ft=ruby :
# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {

:inetRouter => {
      :box_name => "centos/7",
      :net => [
                 {ip: '192.168.255.1', adapter: 2, netmask: "255.255.255.240", virtualbox__intnet: "router-net"},
                 {ip: '192.168.255.1', adapter: 3, netmask: "255.255.255.240", virtualbox__intnet: "router-net"},
              ]
},

:centralRouter => {
      :box_name => "centos/7",
      :net => [
                 {ip: '192.168.255.2', adapter: 2, netmask: "255.255.255.240", virtualbox__intnet: "router-net"},
                 {ip: '192.168.255.2', adapter: 3, netmask: "255.255.255.240", virtualbox__intnet: "router-net"},
                 {ip: '10.10.10.5', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "local"},
              ]
},

:testClient1 => {
      :box_name => "centos/7",
      :net => [
                 {ip: '10.10.10.1', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "local"},
                 
              ]
},

:testServer1 => {
      :box_name => "centos/7",
      :net => [
                 {ip: '10.10.10.254', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "local"},
                 
              ]
},

:testClient2 => {
      :box_name => "centos/7",
      :net => [
                 {ip: '10.10.10.1', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "local"},
                 
              ]
},

:testServer2 => {
      :box_name => "centos/7",
      :net => [
                 {ip: '10.10.10.254', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "local"},
                 
              ]
},
  
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

    config.vm.define boxname do |box|

        box.vm.box = boxconfig[:box_name]
        box.vm.host_name = boxname.to_s

        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end
        
        box.vm.provision "ansible" do |ansible|
          ansible.playbook = "ansible/playbook/provision.yml"
        end
                
    end

  end
    
end