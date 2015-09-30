# -*- mode: ruby -*-
# vi: set ft=ruby :

#Provisioning script for installing Go and setting correct environments
$script = <<SCRIPT
GO_VERSION=1.5.1

echo 'Updating and installing Ubuntu packages...'
sudo apt-get update -qq

echo 'Installing git and mercurial'
sudo apt-get install -y -qq git mercurial

echo 'Downloading go$GO_VERSION.linux-amd64.tar.gz'
wget –quiet https://storage.googleapis.com/golang/go$GO_VERSION.linux-amd64.tar.gz

echo 'Unpacking go language'
sudo tar -C /usr/local -xzf go$GO_VERSION.linux-amd64.tar.gz

echo 'Setting up correct env. variables'
echo "export GOPATH=/vagrant/" >> /home/vagrant/.bashrc
echo "export PATH=\\$PATH:\\$GOPATH/bin:/usr/local/go/bin" >> /home/vagrant/.bashrc

echo 'Installing godep'
export GOPATH=/vagrant/
/usr/local/go/bin/go get -u github.com/tools/godep
SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  # Forwarding port 9900 to local 9900.
  config.vm.network "forwarded_port", guest: 9900, host: 9900
  config.vm.provision "shell", privileged: false, inline: $script
end