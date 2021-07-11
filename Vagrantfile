# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
# Servidor web
  config.vm.define "web" do |web|
		web.vm.hostname = "webserver"
		web.vm.box = "bento/ubuntu-20.04"
		web.vm.network "private_network", ip: "192.168.33.10"
	end
# Servidor Grafana
	config.vm.define "grafana" do |grafana|
    grafana.vm.hostname = "grafanaserver"
    grafana.vm.box = "bento/ubuntu-20.04"
    grafana.vm.network "private_network", ip: "192.168.33.20"
  end
# Servidor de control
	config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.hostname = "ubuntu"
    ubuntu.vm.box = "bento/ubuntu-20.04"
    ubuntu.vm.network "private_network", ip: "192.168.33.100"
    ubuntu.vm.post_up_message = "Welcome to Ubuntu node"

# Provision sobre el Servidor de control
    ubuntu.vm.provision "shell", inline: <<-SHELL
	apt-add-repository ppa:ansible/ansible
	apt-get update
	apt-get -y install sshpass
	apt-get -y install ansible
    ssh-keyscan -H 192.168.33.10 >> /home/vagrant/.ssh/known_hosts
    ssh-keyscan -H 192.168.33.20 >> /home/vagrant/.ssh/known_hosts
    chown vagrant:vagrant /home/vagrant/.ssh/known_hosts
    /etc/init.d/ssh reload
		su vagrant -c "ansible-galaxy collection install community.grafana"
    SHELL
    ubuntu.vm.provision :setup, type: :ansible_local do |ansible|
        ansible.playbook = "main.yml"
        ansible.provisioning_path = "/vagrant"
        ansible.inventory_path = "/vagrant/hosts"
				ansible.limit = :all
    end
  end
end
