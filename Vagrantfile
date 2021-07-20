Vagrant.configure("2") do |config|
	config.vm.define 'linux-hands-on' do |main|
		# https://app.vagrantup.com/ubuntu/boxes/xenial64/versions/20210623.0.0
		main.vm.box = "ubuntu/xenial64"
		main.vm.box_version = "20210623.0.0"
		main.vm.hostname = "linux-hands-on"
	
		# https://www.vagrantup.com/docs/networking/private_network.html
		main.vm.network "private_network", ip: "192.168.33.10"
	
		main.vm.synced_folder "./data", "/vagrant"
	
		# https://www.vagrantup.com/docs/virtualbox/configuration.html#vboxmanage-customizations
		main.vm.provider "virtualbox" do |vb|
		vb.memory = "2048"
		vb.cpus = 2
		end
		# main.vm.provision : shell, path: "provision/bootstrap.sh"
	end
end