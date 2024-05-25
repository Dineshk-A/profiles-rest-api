# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/bionic64"
  config.vm.box_version = "~> 20191107.0.0"
  config.vm.boot_timeout = 1200

  # Forward port 8000 from guest to host
  config.vm.network "forwarded_port", guest: 8000, host: 8000

  # Increase VM resources
  config.vm.provider "virtualbox" do |vb|
    vb.gui = true       # Enable GUI for debugging
    vb.memory = "2048"  # Allocate 2GB of memory
    vb.cpus = 2         # Allocate 2 CPU cores
  end

  # Provisioning script
  config.vm.provision "shell", inline: <<-SHELL
    systemctl disable apt-daily.service
    systemctl disable apt-daily.timer

    sudo apt-get update
    sudo apt-get install -y python3-venv zip
    touch /home/vagrant/.bash_aliases
    if ! grep -q PYTHON_ALIAS_ADDED /home/vagrant/.bash_aliases; then
      echo "# PYTHON_ALIAS_ADDED" >> /home/vagrant/.bash_aliases
      echo "alias python='python3'" >> /home/vagrant/.bash_aliases
    fi
  SHELL
end
