Vagrant.configure("2") do |config|
  config.ssh.insert_key = true
  config.vm.hostname = "ubuntu"
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
  config.vm.provider :docker do |d|
     d.build_dir = "."
     d.remains_running = true
     d.has_ssh = true
  end
#   config.vm.provision :shell, path: "install.sh", privileged: false
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
config.vm.network "private_network", ip: "192.168.33.10"
  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  config.vm.network "forwarded_port", guest: 3389, host: 33890
end
