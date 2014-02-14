VAGRANTFILE_API_VERSION = "2"
Vagrant.require_version ">= 1.4.2"


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	# Use this box when bringing up a new machine
	config.vm.box = "opscode-ubuntu-12.04-i386"
	config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-ubuntu-12.04-i386.box"

	# Which version of chef to use
	config.omnibus.chef_version = :latest
	
	# Forward any ssh keys onward
	config.ssh.forward_agent = true

	# Set up the IP of the new machine 
	config.vm.network "private_network", ip: "192.168.50.4"

	# Tell virtualbox how much memory to allocate
	config.vm.provider "virtualbox" do |v|
		v.memory = 512
	end

	# Use the berkshelf plugin to reach out to berkshelf to make sure we have the cookbooks we need
	config.berkshelf.enabled = true
	config.berkshelf.berksfile_path = "chef-repo/Berksfile"

	# Use chef solo to configure the new machine
	config.vm.provision "chef_solo" do |chef|
		# Enable ONLY for troubleshooting
		#chef.log_level = :debug

		# Where to find various files the chef solo provisioner needs to function
		chef.cookbooks_path = ['chef-repo/cookbooks']

		# Make sure we have the latest/greatest packages
		chef.add_recipe "apt::default"

		# Run our kml to csv recipe
    chef.add_recipe "kml-to-csv"
	end	
end