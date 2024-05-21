Vagrant.configure("2") do |config|
  
  config.vm.define "ubuntu-server" do |machine|
    machine.vm.box = "ubuntu-server-22.04"
    machine.vm.box_url = "C:\\vagrant\\ubuntu-server-22.04.box"
    machine.vm.network "private_network", type: "dhcp"
  end

  config.vm.define "server01"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 2
    vb.customize ["modifyvm", :id, "--name", "server01"]
    vb.customize ["modifyvm", :id, "--nic1", "bridged", "--bridgeadapter1", "Realtek Gaming 2.5GbE Family Controller"]
  end

  config.vm.network "public_network", ip: "192.168.0.27"

  config.vm.provision "shell", inline: <<-SHELL
    echo 'root:111' | chpasswd
    useradd -m -s /bin/bash user01
    echo 'user01:123' | chpasswd
    echo 'user01 ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
  SHELL

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["createhd", "--filename", "disk.vdi", "--size", 10240]
    vb.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 1, "--device", 0, "--type", "hdd", "--medium", "disk.vdi"]
  end
end