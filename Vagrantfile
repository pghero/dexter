Vagrant.configure("2") do |config|
  config.vm.define "xenial" do |c|
    c.vm.box = "ubuntu/xenial64"
    c.vm.provision "shell", inline: <<-SCRIPT
wget -qO - https://deb.packager.io/key | sudo apt-key add -
echo "deb https://deb.packager.io/gh/pghero/dexter xenial master" | sudo tee /etc/apt/sources.list.d/dexter.list
sudo apt-get update
sudo apt-get -y install dexter
    SCRIPT
  end
end
