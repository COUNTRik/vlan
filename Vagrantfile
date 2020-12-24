# -*- mode: ruby -*-
# vim: set ft=ruby :
# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {

# :inetRouter => {
#       :box_name => "centos/7",
#       :net => [
#                  {ip: '192.168.255.1', adapter: 2, netmask: "255.255.255.240", virtualbox__intnet: "router-net"},
#                  {ip: '192.168.255.1', adapter: 3, netmask: "255.255.255.240", virtualbox__intnet: "router-net"},
#               ]
# },

# :centralRouter => {
#       :box_name => "centos/7",
#       :net => [
#                  {ip: '192.168.255.2', adapter: 2, netmask: "255.255.255.240", virtualbox__intnet: "router-net"},
#                  {ip: '192.168.255.2', adapter: 3, netmask: "255.255.255.240", virtualbox__intnet: "router-net"},
#                  {ip: '10.10.10.2', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "test"},
#               ]
# },

# :testClient1 => {
#       :box_name => "centos/7",
#       :net => [
#                  {ip: '10.10.10.1', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 
#               ]
# },

# :testServer1 => {
#       :box_name => "centos/7",
#       :net => [
#                  {ip: '10.10.10.254', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 
#               ]
# },

# :testClient2 => {
#       :box_name => "centos/7",
#       :net => [
#                  {ip: '10.10.10.1', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 
#               ]
# },

# :testServer2 => {
#       :box_name => "centos/7",
#       :net => [
#                  {ip: '10.10.10.254', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 
#               ]
# },

:inetRouter => {
      :box_name => "centos/7",
      :net => [
                 {adapter: 2, virtualbox__intnet: "router-net"},
                 {adapter: 3, virtualbox__intnet: "router-net"},
              ]
},

:centralRouter => {
      :box_name => "centos/7",
      :net => [
                 {adapter: 2, virtualbox__intnet: "router-net"},
                 {adapter: 3, virtualbox__intnet: "router-net"},
                 {ip: '192.168.0.3', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 # {virtualbox__intnet: "test"},
              ]
},

:testClient1 => {
      :box_name => "centos/7",
      :net => [
                 {ip: '192.168.0.1', adapter: 2, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 
              ]
},

:testServer1 => {
      :box_name => "centos/7",
      :net => [
                 {ip: '192.168.0.11', adapter: 2, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 
              ]
},

:testClient2 => {
      :box_name => "centos/7",
      :net => [
                 {ip: '192.168.0.2', adapter: 2, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 
              ]
},

:testServer2 => {
      :box_name => "centos/7",
      :net => [
                 {ip: '192.168.0.22', adapter: 2, netmask: "255.255.255.0", virtualbox__intnet: "test"},
                 
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