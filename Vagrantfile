# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
MEMSIZE = "2048"
NUMCPUS = "1"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "precise64"
    config.vm.box_url = "http://files.vagrantup.com/precise64.box"
    config.vm.network :forwarded_port, guest: 80, host: 8080

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", MEMSIZE]
        vb.customize ["modifyvm", :id, "--cpus", NUMCPUS]
    end

    config.vm.provider :vmware_fusion do |v, override|
        override.vm.box = "precise64_vmware"
        override.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"
        v.vmx["memsize"] = MEMSIZE
        v.vmx["numvcpus"] = NUMCPUS
    end

    config.vm.provision :ansible do |ansible|
        ansible.playbook = "provisioning/playbook.yml"
    end

end
