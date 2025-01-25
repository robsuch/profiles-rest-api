Vagrant.configure("2") do |config|
  config.vm.box = "perk/ubuntu-2204-arm64"
  config.vm.synced_folder ".", "/vagrant", type: "smb", smb_username: "Robert Suchecki", smb_password: "Marcik02", smb_host: "192.168.178.85"
  config.vm.provider "qemu" do |qe|
    qe.ssh_port = "50022" # change ssh port as needed
  end
  config.vm.network "forwarded_port", guest: 8080, host: 8080
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
