# vim: ft=ruby
# Note: This config requires Vagrant 1.1 or higher.
# http://downloads.vagrantup.com

Vagrant.configure("2") do |config|
  config.vm.box = "mediacore-precise64"
  config.vm.box_url = "https://s3.amazonaws.com/mediacore-public/boxes/ec2-precise64.box"

  # Forward SSH Agent
  config.ssh.forward_agent = true

  # Set your VM mem usage here
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "256"]
    # Allow symlinks in vagrant shared folders.
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  # =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
  # Create a Vagrant cluster (or just a single VM)
  #
  # Define an Appserver Ansibling
  config.vm.define :web do |web_config|
    # Set a human readable name for our vm
    web_config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--name", "web"]
    end
    
    # Host Information
	web_config.vm.hostname = "web"

	# Networking
    web_config.vm.network :forwarded_port, guest: 80, host: 8080
	web_config.vm.network "private_network", ip: "192.168.254.254"

	# =-=-==-
    # Provision the box with the builtin vagrant-ansible plugin
	# http://docs.vagrantup.com/v2/provisioning/ansible.html
	# Also, ansible needs to be on your local.
	# For Brew installs, this helps:
	# brew install python
	# brew install pyyaml
	# brew install jinja2
	# brew install https://raw.github.com/mnot/homebrew-stuff/master/ansible.rb
    web_config.vm.provision :ansible do |ansible|
      # What playbook shall we provision the box with?
	  ansible.playbook = 'site.yml'

	  # Where can ansible inventory file be located?
      ansible.inventory_path = 'hosts'

	  # Do we want extra verbosity from Ansible?
      # Note that this doesn't enable "live" output from Ansible :(
      ansible.verbose = 'vvv'
	end

  end

end
