# -*- mode: ruby -*-
# vi: set ft=ruby :

$common = <<SCRIPT

echo "* Add hosts ..."
echo "192.168.100.101 docker-app.prd docker-app" >> /etc/hosts

SCRIPT

Vagrant.configure(2) do |config|
    
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.define "docker" do |docker|
    docker.vm.box = "merev/debian-11"
    docker.vm.box_version = "1"
    docker.vm.hostname = "docker-app.prd"
    docker.vm.network "private_network", ip: "192.168.100.101"
    docker.vm.synced_folder "vagrant/", "/vagrant"
    docker.vm.provision "shell", inline: $common
    docker.vm.provision "shell", path: "docker-setup.sh"
  end

end
