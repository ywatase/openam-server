# -*- mode: ruby -*-
# vi: set ft=ruby :

$vb_memory = 1024 * 2
$vb_cpus   = 1 * 4

Vagrant.configure(2) do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define :openam do |openam|
    openam.vm.box = "centos/7"
    openam.vm.network :private_network, ip:"192.168.52.11"
    openam.vm.hostname = 'openam'
    openam.vm.provider "virtualbox" do |vb|
      vb.name   = 'openam-test-server'
      vb.memory = $vb_memory
      vb.cpus   = $vb_cpus
    end
  end

  config.vm.define :web do |web|
    web.vm.box = "centos/7"
    web.vm.network :private_network, ip:"192.168.52.21"
    web.vm.hostname = 'web'
    web.vm.provider "virtualbox" do |vb|
      vb.name   = 'openam-test-web'
      vb.memory = $vb_memory
      vb.cpus   = $vb_cpus
    end
  end

  config.vm.provision :ansible do |ansible|
    ansible.groups = {
      "local_openam" => ["openam"],
      "local_web"    => ["web"],
    }
    ansible.playbook = "ansible/provision.yml"
    ansible.limit = 'all'
  end
end
