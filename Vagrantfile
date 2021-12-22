Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: <<-SHELL
        apt-get update -y
        echo "192.168.56.10  master-node" >> /etc/hosts
        echo "192.168.56.11  worker-node" >> /etc/hosts
    SHELL
    
    config.vm.define "master" do |master|
      master.vm.box = "generic/ubuntu2004"
      master.vm.hostname = "master-node"
      master.vm.network "private_network", ip: "192.168.56.10"
      master.vm.provider "virtualbox" do |vb|
          vb.memory = 4048
          vb.cpus = 2
      end
      master.vm.provision "shell", path: "scripts/common.sh"
      master.vm.provision "shell", path: "scripts/master.sh"
    end

    config.vm.define "worker" do |node|
      node.vm.box = "generic/ubuntu2004"
      node.vm.hostname = "worker-node"
      node.vm.network "private_network", ip: "192.168.56.11"
      node.vm.provider "virtualbox" do |vb|
          vb.memory = 2048
          vb.cpus = 1
      end
      node.vm.provision "shell", path: "scripts/common.sh"
      node.vm.provision "shell", path: "scripts/node.sh"
    end
  end