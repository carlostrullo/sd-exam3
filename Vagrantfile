# -*- mode: ruby -*-
# vi: set ft=ruby :
 
VAGRANTFILE_API_VERSION = "2"
 
disk1 = './disk1.vdi'
disk2 = './disk2.vdi'
disk3 = './disk3.vdi'
 
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  config.vm.define :mestro do |server|
    server.vm.box = "ThomasHack/ubuntu16lts-apache2-php7-mysql"
    server.vm.box_version = "1.1.4"
    server.vm.network :private_network, ip: "192.168.33.115"
    server.vm.provider :virtualbox do |vb|
      vb.gui = true 
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "maestro" ]
      unless File.exist?(disk1)
        vb.customize ['createhd', '--filename', disk1, '--variant', 'Fixed', '--size', 5120]
      end
      vb.customize ['storageattach', :id,  '--storagectl', 'SCSI', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk1]
    end
    server.vm.provision "shell", inline: <<-SHELL
      echo "server" > /etc/hostname
      hostname server
    SHELL
    server.vm.provision "shell", path: "scripts/config.sh"
    server.vm.provision "shell", path: "scripts/docker.sh"
    server.vm.provision "shell", path: "scripts/glusterfs.sh"
  end

  config.vm.define :nodo_Uno do |nodo_1|
    nodo_1.vm.box = "ThomasHack/ubuntu16lts-apache2-php7-mysql"
    nodo_1.vm.box_version = "1.1.4"
    nodo_1.vm.network :private_network, ip: "192.168.33.116"
    nodo_1.vm.provider :virtualbox do |vb|
      vb.gui = true 
      vb.customize ["modifyvm", :id, "--memory", "512","--cpus", "1", "--name", "nodo_Uno" ]
      unless File.exist?(disk2)
        vb.customize ['createhd', '--filename', disk2, '--variant', 'Fixed', '--size', 5120]
      end
      vb.customize ['storageattach', :id,  '--storagectl', 'SCSI', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk2]
    end
    nodo_1.vm.provision "shell", inline: <<-SHELL
      echo "nodo_1" > /etc/hostname
      hostname nodo_1
    SHELL
    nodo_1.vm.provision "shell", path: "scripts/config.sh"
    nodo_1.vm.provision "shell", path: "scripts/docker.sh"
    nodo_1.vm.provision "shell", path: "scripts/glusterfs.sh"
  end

  
  config.vm.define :nodo_Dos do |nodo_2|
    nodo_2.vm.box = "ThomasHack/ubuntu16lts-apache2-php7-mysql"
    nodo_2.vm.box_version = "1.1.4"
    nodo_2.vm.network :private_network, ip: "192.168.33.117"
    nodo_2.vm.provider :virtualbox do |vb|
      vb.gui = true 
      vb.customize ["modifyvm", :id, "--memory", "512","--cpus", "1", "--name", "nodo_Dos" ]
      unless File.exist?(disk3)
        vb.customize ['createhd', '--filename', disk3, '--variant', 'Fixed', '--size', 5120]
      end
      vb.customize ['storageattach', :id,  '--storagectl', 'SCSI', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk3]
    end
    nodo_2.vm.provision "shell", inline: <<-SHELL
      echo "nodo_2" > /etc/hostname
      hostname nodo_2
    SHELL
    nodo_2.vm.provision "shell", path: "scripts/config.sh"
    nodo_2.vm.provision "shell", path: "scripts/docker.sh"
    nodo_2.vm.provision "shell", path: "scripts/glusterfs.sh"
  end
end
