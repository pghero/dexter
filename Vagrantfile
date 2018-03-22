Vagrant.configure("2") do |config|
  config.vm.define "xenial" do |c|
    c.vm.box = "ubuntu/xenial64"
    c.vm.provision "shell", inline: <<-SCRIPT
# dexter
wget -qO - https://deb.packager.io/key | sudo apt-key add -
echo "deb https://deb.packager.io/gh/pghero/dexter xenial master" | sudo tee /etc/apt/sources.list.d/dexter.list
sudo apt-get update
sudo apt-get -y install dexter

# postgres and movielens data
sudo apt-get -y install postgresql
sudo -u postgres createdb movielens
wget -qO- https://raw.githubusercontent.com/ankane/movielens.sql/master/movielens.sql | sudo -u postgres psql -d movielens

# hypopg
sudo apt-get -y install postgresql-server-dev-9.5 make gcc
wget https://github.com/HypoPG/hypopg/archive/1.1.0.tar.gz
tar xf 1.1.0.tar.gz
cd hypopg-1.1.0
make
sudo make install

# test
sudo -u postgres dexter movielens -s "SELECT * FROM ratings WHERE user_id = 1"
    SCRIPT
  end

  config.vm.define "jessie" do |c|
    c.vm.box = "debian/jessie64"
    c.vm.provision "shell", inline: <<-SCRIPT
# dexter
sudo apt-get -y install apt-transport-https
wget -qO- https://dl.packager.io/srv/pghero/dexter/key | sudo apt-key add -
sudo wget -O /etc/apt/sources.list.d/dexter.list \
  https://dl.packager.io/srv/pghero/dexter/master/installer/debian/8.repo
sudo apt-get update
sudo apt-get -y install dexter

# postgres and movielens data
sudo apt-get -y install postgresql
sudo -u postgres createdb movielens
wget -qO- https://raw.githubusercontent.com/ankane/movielens.sql/master/movielens.sql | sudo -u postgres psql -d movielens

# hypopg
sudo apt-get -y install postgresql-server-dev-9.4 make gcc
wget https://github.com/HypoPG/hypopg/archive/1.1.0.tar.gz
tar xf 1.1.0.tar.gz
cd hypopg-1.1.0
make
sudo make install

# test
sudo -u postgres dexter movielens -s "SELECT * FROM ratings WHERE user_id = 1"
    SCRIPT
  end
end
