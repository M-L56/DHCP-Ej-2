# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox"

  config.vm.define "server" do |s|
    s.vm.box = "debian/bookworm64"
    s.vm.network "private_network", ip: "192.168.56.10"
    s.vm.network "private_network", ip: "192.168.57.10",
      virtualbox__intnet: true
    s.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y isc-dhcp-server
      sudo echo INTERFACESv4="eth2" > /etc/default/isc-dhcp-server
      cp -vf /vagrant/ConfigDHCP/dhcpd.conf /etc/dhcp/
      systemctl restart isc-dhcp-server
    SHELL
  end #Server
  
  config.vm.define "c1" do |c1|
    c1.vm.box = "debian/bookworm64"
    c1.vm.network "private_network",
      #:mac => "5CA1AB1E0001",
      auto_config: false,
      virtualbox__intnet: true
    c1.vm.provision "shell", inline: "dhclient eth1"
  end #Client

  config.vm.define "c2" do |c2|
    c2.vm.box = "debian/bookworm64"
    c2.vm.network "private_network",
      mac:"5CA1AB1E0001",
      auto_config: false,
      virtualbox__intnet: true
    c2.vm.provision "shell", inline: "dhclient eth1"
  end #Client

  
end
