# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |cluster|
	(2..3).each do |index|
		last_octet = index * 10
		cluster.vm.define "vm#{index}" do |config|
      config.vm.box = "bryanhuntesl/alpine64"
			config.vm.box_version = "3.8.2"
      config.vm.provider :vmware_fusion do |vm, override|
        vm.vmx["memsize"] = "1024"
        vm.vmx["numvcpus"] = "1"
      end
      config.vm.hostname = "k8s1"
      config.ssh.shell = "/bin/ash"
      config.vm.network "private_network", ip: "33.33.34.#{index}", type: "dhcp", auto_config: true
      ssh_port = Random.new.rand(1000...5000)
      config.vm.network "forwarded_port", guest: 22, host: "#{ssh_port}", id: 'ssh', auto_correct: true
			config.vm.synced_folder ".", "/vagrant", disabled: true
			config.vm.provision "shell", inline: <<-SHELL
				echo "hello world"
			SHELL
		end
  end
end
