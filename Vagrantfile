# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu1804"
  config.vm.synced_folder "./", "/Vagrant"

  config.vm.define "gitlab" do |gitlab|
    gitlab.vm.hostname = "gitlab"
    gitlab.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
    gitlab.vm.network "private_network", ip: "192.168.33.10"

    gitlab.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
    end

    gitlab.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y curl openssh-server ca-certificates 
      
      curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash

      EXTERNAL_URL="http://gitlab.example.com" apt-get install gitlab-ee

      gitlab-ctl reconfigure
    SHELL
  end

  config.vm.define "ldap" do |ldap|
    ldap.vm.hostname = "ldap"
    ldap.vm.network "private_network", ip: "192.168.33.20"

    ldap.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
    end

    # ldap.vm.provision "shell", inline: <<-SHELL
    #   apt update
    #   apt -y install slapd ldap-utils
    # SHELL
  end
end
