# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :


# VM box image
VAGRANT_BOX = 'ubuntu/trusty64'
# Memorable name for your
VM_NAME = 'web-server'
# VM User — 'vagrant' by default
VM_USER = 'vagrant'   
# Username on your Mac
MAC_USER = 'tarek'
# Host folder to sync
HOST_PATH = '/Users/tarek/Documents/shared/' + VM_NAME   
# Where to sync to on Guest — 'vagrant' is the default user name
GUEST_PATH = '/home/' + VM_USER + '/' + VM_NAME

# Vagrant box from Hashicorp
Vagrant.configure(2) do |config|
  config.vm.box = VAGRANT_BOX
  
  # Actual machine name
  # Set VM name in Virtualbox
  config.vm.hostname = VM_NAME
  config.vm.provider "virtualbox" do |v|
    v.name = VM_NAME
    v.memory = 4096
  end
  
  # PRIVATE NETWORK — set private network with static ip
  config.vm.network "private_network", ip: "192.168.50.10",
    virtualbox__intnet: "private_network"

  # Disable default Vagrant folder, use a unique path per project
  config.vm.synced_folder HOST_PATH, GUEST_PATH
  config.vm.synced_folder '.', '/home/' + VM_USER + '', disabled: true 
  # Install apache2
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git
    apt-get upgrade -y
    apt-get autoremove -y
    apt-get install apache2
  SHELL
end

