# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	# Every Vagrant virtual environment requires a box to build off of.
	config.vm.box = "ubuntu/trusty64"

	config.berkshelf.enabled = true
	config.omnibus.chef_version = "11.16.4"

	config.vm.network :forwarded_port, guest: 8125, host: 8125, protocol: 'udp'
	config.vm.network :forwarded_port, guest: 8126, host: 8126
	config.vm.network :forwarded_port, guest: 2003, host: 2003
	config.vm.network :forwarded_port, guest: 2004, host: 2004

	config.vm.provision :chef_solo do |chef|
		#chef.add_recipe "graphite::carbon"
		chef.add_recipe "statsd"
		chef.add_recipe "metrics"
		chef.json =  {statsd: {
				nodejs_bin: "/usr/bin/node"
			}
		}
	end

	config.vm.provider :virtualbox do |vb|
		vb.name = "metrics"
	end

end
