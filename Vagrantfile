# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

   config.vm.box = "ubuntu-14.4"
   config.vm.box_url = "https://atlas.hashicorp.com/ubuntu/boxes/trusty64/versions/20160802.0.1/providers/virtualbox.box"
   config.ssh.forward_agent = true

   config.hostmanager.enabled = true
   config.hostmanager.manage_host = false
   config.hostmanager.ignore_private_ip = true
   config.hostmanager.include_offline = true

   config.vm.hostname = "beautymove"

   config.vm.network :private_network, ip: "192.168.33.10"

   config.hostmanager.aliases = %w(beautymove.local)

   config.vm.synced_folder ".", "/var/www", mount_options: ['dmode=777','fmode=666']

   config.vm.provider :virtualbox do |vb|
       # Use VBoxManage to customize the VM.
       # For example to change memory or number of CPUs:
       vb.customize ["modifyvm", :id, "--memory", "1024"]
       vb.customize ["modifyvm", :id, "--cpus", "1"]
   end

   config.vm.provision "shell", path: "provision/puppet/scripts/ubuntu.sh"

   config.vm.provision :puppet do |puppet|
       puppet.manifests_path = "provision/puppet/manifests"
       puppet.manifest_file = "site.pp"
       puppet.module_path = "provision/puppet/modules"
       puppet.options = "--verbose --debug"
   end

end
