Vagrant.configure("2") do |config|

  config.vm.define "dev01nginx" do |dev01nginx|
    dev01nginx.vm.box = "generic/ubuntu2004"
    dev01nginx.vm.hostname = "ubuntu-dev01nginx"
    dev01nginx.vm.provider "hyperv" do |hv|
      hv.memory = 4096
      hv.maxmemory = 4096 
      hv.cpus = 2
      hv.vmname = "dev01nginx"
    end
    dev01nginx.vm.synced_folder ".", "/vagrant", type: "smb"
    dev01nginx.vm.synced_folder "web", "/var/www/html", type: "smb"
    dev01nginx.vm.network "public_network"
    dev01nginx.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update 
      sudo apt-get install -y openssh-server

      # Write Netplan configuration file with echo
      sudo echo 'network:' > /etc/netplan/01-netcfg.yaml
      sudo echo '  version: 2' >> /etc/netplan/01-netcfg.yaml
      sudo echo '  renderer: networkd' >> /etc/netplan/01-netcfg.yaml
      sudo echo '  ethernets:' >> /etc/netplan/01-netcfg.yaml
      sudo echo '    eth0:' >> /etc/netplan/01-netcfg.yaml
      sudo echo '      dhcp4: true' >> /etc/netplan/01-netcfg.yaml
      sudo echo '    eth1:' >> /etc/netplan/01-netcfg.yaml
      sudo echo '      dhcp4: false' >> /etc/netplan/01-netcfg.yaml
      sudo echo '      addresses: [192.168.69.11/24]' >> /etc/netplan/01-netcfg.yaml

      # Apply the changes
      sudo netplan apply
    SHELL
  end
  
end