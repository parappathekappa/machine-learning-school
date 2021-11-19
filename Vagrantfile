# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.host_name = 'chipsite-development'

  config.vm.network "private_network", type: "dhcp"
  config.vm.synced_folder ".", "/vagrant", type: "nfs",
    mount_options: ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2']

  # Bootstrap system requirements + app
  config.vm.provision :shell, path: "scripts/bootstrap-env.sh"
  config.vm.provision :shell, path: "scripts/bootstrap-app.sh", privileged: false

  # expose dev server @ http://localhost:8000
  config.vm.network "forwarded_port", guest: 8000, host: 8000

  # expose postgres
  config.vm.network "forwarded_port", guest: 5432, host: 8432

  config.vm.provider "virtualbox" do |v|
    v.memory = 4096 # 2GB rams
  end
end
