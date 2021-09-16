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

		# peco
		wget https://github.com/peco/peco/releases/download/v0.5.10/peco_linux_amd64.tar.gz
		tar zxvf ./peco_linux_amd64.tar.gz
		cp ./peco_linux_amd64/peco /usr/local/bin/
		# TODO: ~/.bashrc に以下を追記する
		##  重複履歴を無視
		# export HISTCONTROL=ignoreboth:erasedups
		# export HISTSIZE=10000

		##  settings for peco
		# function peco-select-history() {
		# 	local tac
		# 	which gtac &> /dev/null && tac="gtac" || \
		# 		which tac &> /dev/null && tac="tac" || \
		# 		tac="tail -r"
		# 	READLINE_LINE=$(HISTTIMEFORMAT= history | $tac | sed -e 's/^\s*[0-9]\+\s\+//' | awk '!a[$0]++' | peco --query "$READLINE_LINE")
		# 	READLINE_POINT=${#READLINE_LINE}
		# 	}
		# bind -x '"\C-r":peco-select-history'
		source ~/.bashrc
		SCRIPT

		main.vm.provision "shell", inline: $script
	end
end