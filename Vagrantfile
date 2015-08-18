Vagrant.configure("2") do |config|
  config.vm.box = "opscode-debian-8.1"
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_debian-8.1_chef-provisionerless.box"
  config.vm.hostname = "freetz"

  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 2
    v.customize ["modifyvm", :id, "--name", "freetz"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/provision.yml"
    #ansible.extra_vars = { freetz_svn_url: 'http://svn.freetz.org/branches/freetz-stable-2.0' }
    ansible.extra_vars = { freetz_svn_url: 'http://svn.freetz.org/trunk' }
  end

end
