Vagrant.configure("2") do |config|
	config.vm.define 'linux-hands-on' do |main|
		# https://app.vagrantup.com/ubuntu/boxes/focal64/versions/20210811.0.0
		main.vm.box = "ubuntu/focal64"
		main.vm.box_version = "20210811.0.0"		
		main.vm.hostname = "linux-hands-on"
	
		# https://www.vagrantup.com/docs/networking/private_network.html
		main.vm.network "private_network", ip: "192.168.33.10"
	
		main.vm.synced_folder "./data", "/vagrant"
	
		# https://www.vagrantup.com/docs/virtualbox/configuration.html#vboxmanage-customizations
		main.vm.provider "virtualbox" do |vb|
			vb.memory = "2048"
			vb.cpus = 2
		end

		# 2回目以降の起動時に provision を走らせたい場合
		# vagrant up --provision
		$script = <<-SCRIPT
		apt update -y
		apt-get install -y gcc sysstat openjdk-11-jdk net-tools
		
		# for use sar command
		sed -ie 's/ENABLED="false"/ENABLED="true"/' /etc/default/sysstat
		/etc/init.d/sysstat start
		SCRIPT

		main.vm.provision "shell", inline: $script
	end
end