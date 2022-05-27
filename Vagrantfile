# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  ## controller node
  config.vm.define "controller" do |cfg|
    cfg.vm.box = "centos/7"

    parityDisk = 'controllerParityDisk.vdi'
    dataDisk1 = 'controllerDataDisk1.vdi'
    dataDisk2 = 'controllerataDisk2.vdi'


    cfg.vm.provider "virtualbox" do |vb|
      vb.name = "Controller"
      vb.memory = "4096"

      # Building disk files if they don't exist
      if not File.exists?(parityDisk)
        vb.customize ['createhd', '--filename', parityDisk, '--variant', 'Fixed', '--size', 30 * 1024]
      end
      if not File.exists?(dataDisk1)
        vb.customize ['createhd', '--filename', dataDisk1, '--variant', 'Fixed', '--size', 20 * 1024]
      end
      if not File.exists?(dataDisk2)
        vb.customize ['createhd', '--filename', dataDisk2, '--variant', 'Fixed', '--size', 2 * 1024]       
      end
      
      # Adding a SATA controller that allows 4 hard drives
      vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 4]
      # Attaching the disks using the SATA controller
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', parityDisk]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', dataDisk1]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', dataDisk2]

      
    end  
    

    cfg.vm.host_name ="controller.ni2"
    cfg.vm.network "public_network", ip: "192.168.1.10"
    cfg.vm.network "forwarded_port", guest:22, host:60011, auto_correct:true, id:"ssh"
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
    cfg.vm.provision "shell", path: "bash_ssh_conf_4_centos.sh"
    cfg.vbguest.auto_update = false
  end  

  ## compute node
  config.vm.define "compute" do |cfg|
    cfg.vm.box = "centos/7"

    parityDisk = 'computeParityDisk.vdi'
    dataDisk1 = 'computeDataDisk1.vdi'
    dataDisk2 = 'computeDtaDisk2.vdi'


    cfg.vm.provider "virtualbox" do |vb|
      vb.name = "Compute"
      vb.memory = "4096"

      # Building disk files if they don't exist
      if not File.exists?(parityDisk)
        vb.customize ['createhd', '--filename', parityDisk, '--variant', 'Fixed', '--size', 30 * 1024]
      end

      if not File.exists?(dataDisk1)
        vb.customize ['createhd', '--filename', dataDisk1, '--variant', 'Fixed', '--size', 20 * 1024]
      end

      if not File.exists?(dataDisk2)
        vb.customize ['createhd', '--filename', dataDisk2, '--variant', 'Fixed', '--size', 20 * 1024]
      end
      
      
      # Adding a SATA controller that allows 4 hard drives
      vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 3]
      # Attaching the disks using the SATA controller
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', parityDisk]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', dataDisk1]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', dataDisk2]
            
    end  
    

    cfg.vm.host_name ="compute.ni2"
    cfg.vm.network "public_network", ip: "192.168.1.11"
    cfg.vm.network "forwarded_port", guest:22, host:60012, auto_correct:true, id:"ssh"
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
    cfg.vm.provision "shell", path: "bash_ssh_conf_4_centos.sh"
    cfg.vbguest.auto_update = false
  end

  ## network node
  config.vm.define "network" do |cfg|
    cfg.vm.box = "centos/7"

    parityDisk = 'networkParityDisk.vdi'
    dataDisk1 = 'networkDataDisk1.vdi'
    dataDisk2 = 'networkDataDisk2.vdi'
    dataDisk3 = 'networkDataDisk3.vdi'


    cfg.vm.provider "virtualbox" do |vb|
      vb.name = "Network"
      vb.memory = "2048"

      # Building disk files if they don't exist
      if not File.exists?(parityDisk)
        vb.customize ['createhd', '--filename', parityDisk, '--variant', 'Fixed', '--size', 20 * 1024]
      end
      if not File.exists?(dataDisk1)
        vb.customize ['createhd', '--filename', dataDisk1, '--variant', 'Fixed', '--size', 20 * 1024]
      end

      if not File.exists?(dataDisk2)
        vb.customize ['createhd', '--filename', dataDisk2, '--variant', 'Fixed', '--size', 20 * 1024]
      end

      if not File.exists?(dataDisk3)
        vb.customize ['createhd', '--filename', dataDisk3, '--variant', 'Fixed', '--size', 10 * 1024]
      end
      
      
      # Adding a SATA controller that allows 4 hard drives
      vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 4]
      # Attaching the disks using the SATA controller
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', parityDisk]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', dataDisk1]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', dataDisk2]
      vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', 4, '--device', 0, '--type', 'hdd', '--medium', dataDisk3]

            
    end  
    

    cfg.vm.host_name ="network.ni2"
    cfg.vm.network "public_network", ip: "192.168.1.12"
    cfg.vm.network "forwarded_port", guest:22, host:60013, auto_correct:true, id:"ssh"
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
    cfg.vm.provision "shell", path: "bash_ssh_conf_4_centos.sh"
    cfg.vbguest.auto_update = false
  end

end
