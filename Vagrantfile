Vagrant.configure("2") do |config|
	config.vm.box = "debian7.2"
	config.vm.box_url = "https://dl.dropboxusercontent.com/u/197673519/debian-7.2.0.box"

	config.vm.network :private_network, ip: "192.168.57.111"

	config.vm.provider :virtualbox do |v|
		v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
		v.customize ["modifyvm", :id, "--memory", 512]
		v.customize ["modifyvm", :id, "--name", "freetz-vm"]
	end

	config.vm.synced_folder "./freetzsrc", "/freetz"

	config.vm.provision "ansible" do |ansible|
		ansible.playbook = "ansible/provision.yml"
	end

end
