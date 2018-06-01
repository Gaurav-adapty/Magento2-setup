# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "geerlingguy/ubuntu1604"
  config.vm.hostname = "magento2-box"
  config.vm.network "private_network", ip: "192.168.1.115"

  # Virtual box config
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = 2
    vb.customize ["modifyvm", :id, "--name", "magento2-box"]
  end

  # Ansible playbook
  config.vm.synced_folder ".", "/vagrant", type: 'virtualbox'

  config.vm.synced_folder "./ecs", "/home/vagrant/repos/magento2", type: 'virtualbox'
  # Host -> Guest NFS
  # config.vm.synced_folder "../magento2", "/home/vagrant/repos/magento2",
  #  type: 'nfs', mount_options: ['rw', 'async', 'fsc' ,'actimeo=2']

  # Provisioning
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    ansible.verbose = "vvvv"
    ansible.extra_vars = "ansible/group_vars/dev.yml"
  end
end
