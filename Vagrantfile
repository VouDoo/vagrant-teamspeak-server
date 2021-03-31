#!/usr/bin/ruby
# -*- mode: ruby -*-


# Vagrantfile
#
# DESCRIPTION
# ~~~~~~~~~~~
# Deploy a Teamspeak server
#
# NOTES
# ~~~~~
# This Vagrantfile uses VirtualBox as provider
# Make sure that VirtualBox is installed on your machine
# To install it, please visit the official Website:
#   https://www.virtualbox.org/wiki/Downloads
#
# Use the following command to spin up the boxes:
#   vagrant up


Vagrant.configure("2") do |config|
  # Provision TeamSpeak server instance
  config.vm.define "ts-server-instance" do |i|
    # Vagrant box - CentOS 7
    i.vm.box = "centos/7"
    # Define hostname
    i.vm.hostname = "ts-server"
    # Set provider settings
    i.vm.provider "virtualbox" do |v|
      v.name = "ts-server"
      v.cpus = 1
      v.memory = 2048
    end
    # Assign IP via DHCP
    i.vm.network "public_network"
    # Install TeamSpeak server
    i.vm.provision "shell", path: "scripts/installApp.sh"
    # Set TeamSpeak service into systemd and start it
    i.vm.provision "shell", path: "scripts/addSystemdService.sh"
    # Create TeamSpeak service into firewalld
    i.vm.provision "shell", path: "scripts/addFirewalldService.sh"
  end
end
