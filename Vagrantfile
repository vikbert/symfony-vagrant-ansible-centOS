# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # base configure
  config.ssh.forward_agent = true
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true

  # vm box configure
  config.vm.define "vagrant-ansible-symfony" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "symfony-dev-box"
    node.vm.network "private_network", ip: "10.10.200.200"
    node.hostmanager.aliases = [
      "symfony.dev",
      "symfony.local",
    ]

    # synced_folder configure
    node.vm.synced_folder ".", "/vagrant", disabled: true
    node.vm.synced_folder "ansible", "/opt/dev/ansible"
    node.vm.synced_folder "vars", "/opt/dev/scripts"
    node.vm.synced_folder "platform", "/var/www/platform",
      :nfs => true,
      :mount_options => ["actimeo=2"]

    # hardware customizing
    node.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
      v.customize ["modifyvm", :id, "--memory", 4096]
      v.customize ["modifyvm", :id, "--cpus", 2]
      v.customize ["modifyvm", :id, "--name", "symfony-dev-box"]
    end


  end
end
