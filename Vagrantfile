Vagrant.configure("2") do |config|
  config.vm.box = "centos64-x64-vbox43-1383512148"
  config.vm.box_url = "http://box.puphpet.com/centos64-x64-vbox43.box"

  config.vm.network "private_network", ip: "10.0.0.100"


  config.vm.synced_folder "./", "/var/www", id: "vagrant-root", :nfs => true

  config.vm.usable_port_range = (2200..2250)
  config.vm.provider :virtualbox do |virtualbox|
    virtualbox.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    virtualbox.customize ["modifyvm", :id, "--memory", "512"]
    virtualbox.customize ["setextradata", :id, "--VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  config.vm.provision :shell, :path => "puphpet/shell/initial-setup.sh"
  config.vm.provision :shell, :path => "puphpet/shell/update-puppet.sh"
  config.vm.provision :shell, :path => "puphpet/shell/librarian-puppet-vagrant.sh"
  config.vm.provision :puppet do |puppet|
    puppet.facter = {
      "ssh_username" => "vagrant"
    }

    puppet.manifests_path = "puphpet/puppet/manifests"
    puppet.options = ["--verbose", "--hiera_config /vagrant/puphpet/puppet/hiera.yaml", "--parser future"]
  end




  config.ssh.username = "vagrant"

  config.ssh.shell = "bash -l"

  config.ssh.keep_alive = true
  config.ssh.forward_agent = false
  config.ssh.forward_x11 = false
  config.vagrant.host = :detect
end

