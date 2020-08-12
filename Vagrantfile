IMAGE_NAME = "bento/centos-8.1"


Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
	config.vm.define "manager" do |vm1|
	    vm1.vm.hostname = "manager"
	    vm1.vm.box = IMAGE_NAME
	    vm1.vm.network "private_network", ip: "192.168.50.10"
		vm1.persistent_storage.enabled = true
		vm1.persistent_storage.location = "C:/temp/sourcehdd.vdi"
		vm1.persistent_storage.size = 50
		vm1.persistent_storage.mountname = 'docker'
		vm1.persistent_storage.filesystem = 'ext4'
		vm1.persistent_storage.mountpoint = '/docker'
		vm1.persistent_storage.volgroupname = 'techchallenge'
	
	    vm1.vm.provider "virtualbox" do |v|
            v.memory = 2048
            v.cpus = 1
		    v.gui = false
        end
		
		vm1.vm.provision :shell, inline: "sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config; service sshd restart"
		vm1.vm.provision :shell, inline: "sudo timedatectl set-timezone Asia/Bangkok"
		vm1.vm.provision :shell, inline: <<-SHELL
			yum update -y
			yum install epel-release -y
			yum install ansible -y
			chmod 666 /etc/ansible/hosts
			cat /vagrant/inventory >> /etc/ansible/hosts
			chmod 444 /etc/ansible/hosts
		SHELL
    end
	
	config.vm.define "worker01" do |vm1|
	    vm1.vm.hostname = "worker01"
	    vm1.vm.box = IMAGE_NAME
	    vm1.vm.network "private_network", ip: "192.168.50.11"
		vm1.persistent_storage.enabled = true
		vm1.persistent_storage.location = "C:/temp/sourcehdd_01.vdi"
		vm1.persistent_storage.size = 50
		vm1.persistent_storage.mountname = 'docker'
		vm1.persistent_storage.filesystem = 'ext4'
		vm1.persistent_storage.mountpoint = '/docker'
		vm1.persistent_storage.volgroupname = 'techchallenge'
	
	    vm1.vm.provider "virtualbox" do |v|
            v.memory = 2048
            v.cpus = 1
		    v.gui = false
        end
		
		vm1.vm.provision :shell, inline: "sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config; service sshd restart"
		vm1.vm.provision :shell, inline: "sudo timedatectl set-timezone Asia/Bangkok"
		vm1.vm.provision :shell, inline: <<-SHELL
			yum update -y
			yum install epel-release -y
			yum install ansible -y
		SHELL
    end
end
