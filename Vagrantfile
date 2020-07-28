# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  
  config.vm.provision "shell",
        inline: <<-F00
                  echo "Vm pour la Mise en Situation 2"
                  F00

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  
  
  
  config.vm.post_up_message = "VM UbuntuBox with Vagrant Ok"
  config.vm.box = "bento/ubuntu-20.04"
  #config.vm.box = "UbuntuBox"

  #config.vm.post_up_message = "VM UbuntuBox with Vagrant Ok"
  #config.vm.box = "debian/buster64"
  #config.vm.box = "DebyBox"


  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 80, host: 8085, host_ip: "127.0.0.1"
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  #### Interface bridge
  
  config.vm.network "public_network", bridge: "en1: Wi-Fi (AirPort)"
  #### DHCP
  config.vm.network "private_network", type: "dhcp"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "/tmp/vagrant_2", "/home/stagiaire/Mise_en_situation-2/Docs"


  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #

  #########  UbuntuBox  #########

		  config.vm.provider "virtualbox" do |vb|

  #   # Customize the name on the VM:
		  vb.name = "UbuntuBox"
		  #vb.name = "DebyBox"
		  
  #   # Display the VirtualBox GUI when booting the machine
		  vb.gui = true

  #   # Customize the amount of memory on the VM:
		  vb.memory = "4096"

  #   # Customize the cpu on the VM:
		  vb.cpus = 2
		  
  #   # Customize the Storage on the VM:
#		  vb.disksize.size = "40GB"

                  end

  #   # Enable provisioning with a shell script. Additional provisioners such as
		  ## add Users
		  config.vm.provision "shell",
				inline: <<-FUser
							sudo useradd -m -s /bin/bash -U yassen -u 666 --groups wheel
							sudo passwd roottoor
							cp -pr /home/vagrant/.ssh /home/yassen/
							chown -R yassen:yassen /home/yassen
							echo "%yassen ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/yassen
							FUser
		  
		  ## add Ngnix
		  config.vm.provision "shell",
				inline: <<-FNginx
							apt-get update
							apt-get install -y nginx
							FNginx
							
		  ## add Gui on Ubuntu				
		  config.vm.provision "shell",
				inline: <<-FGui				
							sudo tasksel ubuntu-desktop
							sudo systemctl isolate graphical
							sudo systemctl set-default graphical.target
							FGui
							
		  ## add Chrome on Ubuntu				
		  config.vm.provision "shell",
				inline: <<-FChrome				
							wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
							sudo apt install ./google-chrome-stable_current_amd64.deb
							FChrome

  end
