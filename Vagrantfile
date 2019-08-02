# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.define :ansible_server do |server_conf|
    server_conf.vm.hostname = "ansible-server"
    server_conf.vm.network :private_network, ip:"192.168.30.11"
    server_conf.vm.synced_folder "./data", "/vagrant_data"
    server_conf.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "1024"
    end

    server_conf.vm.provision "shell", inline: <<-SHELL
      apt update
      apt install -y software-properties-common
      apt-add-repository --yes --update ppa:ansible/ansible
      apt install -y ansible
    SHELL
  end

  config.vm.define :web do |web|
    web.vm.hostname = "web"
    web.vm.network :private_network, ip:"192.168.30.12"
    web.vm.network "forwarded_port", guest: 80, host: 8080
  end
end
