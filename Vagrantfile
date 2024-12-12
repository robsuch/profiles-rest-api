# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

require 'logger'
#log = logger.new(STDOUT)
log = Logger.new("vagrant.log")
log.level = Logger::INFO

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "perk/ubuntu-2204-arm64"
  config.vm.synced_folder ".", "/vagrant", type: "rsync",rsync_auto: true
  config.vm.provider "qemu" do |qe|
    qe.ssh_port = "50023" # change ssh port as needed
  end

  
  log.info("test 1")
  config.vm.provision "shell", inline: <<-SHELL
      systemctl disable apt-daily.service
      systemctl disable apt-daily.timer
    
      sudo apt-get update
    ś
      sudo apt-get install -y python3-venv zip
      touch /home/vagrant/.bash_aliases
      if ! grep -q PYTHON_ALIAS_ADDED /home/vagrant/.bash_aliases; then
        echo "# PYTHON_ALIAS_ADDED" >> /home/vagrant/.bash_aliases
        echo "alias python='python3'" >> /home/vagrant/.bash_aliases
      fi
    SHELL
end
