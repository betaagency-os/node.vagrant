# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "192.168.56.66"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    debconf-set-selections <<< 'mysql-server-5.5 mysql-server/root_password password vagrant'
    debconf-set-selections <<< 'mysql-server-5.5 mysql-server/root_password_again password vagrant'

    cd

    mkdir /home/vagrant/.ssh
    cp /vagrant/_home/.ssh/id_rsa* /home/vagrant/.ssh
    cp /vagrant/_home/.gitconfig /home/vagrant
    cp /vagrant/install /home/vagrant/install
    chomod +x /home/vagrant/install
    chown -R vagrant:vagrant /home/vagrant
  SHELL
end
