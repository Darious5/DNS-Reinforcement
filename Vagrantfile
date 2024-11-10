Vagrant.configure("2") do |config|
  # Configuración del servidor DNS Maestro (DNSA)
  config.vm.define "DNSA" do |dnsa|
    dnsa.vm.box = "debian/bookworm64"
    dnsa.vm.network "private_network", ip: "192.168.57.10"
    dnsa.vm.provision "shell", inline: <<-SHELL
      sudo apt update && sudo apt install -y bind9 dnsutils
      
      
      sudo chown -R vagrant:vagrant /etc/bind
      sudo chmod -R 755 /etc/bind
      
      
      sudo cp /vagrant/configs/named.conf.local.DNSA /etc/bind/named.conf.local
      sudo cp /vagrant/configs/db.ies.test.informatica /etc/bind/db.ies.test.informatica
      sudo cp /vagrant/configs/db.ies.test.aulas /etc/bind/db.ies.test.aulas
      sudo cp /vagrant/configs/db.ies.test.departamentos /etc/bind/db.ies.test.departamentos
      
      
      sudo systemctl restart bind9
    SHELL
  end

  # Configuración del servidor DNS Esclavo (DNSB)
  config.vm.define "DNSB" do |dnsb|
    dnsb.vm.box = "debian/bookworm64"
    dnsb.vm.network "private_network", ip: "192.168.57.11"
    dnsb.vm.provision "shell", inline: <<-SHELL
      sudo apt update && sudo apt install -y bind9 dnsutils
      
      
      sudo chown -R vagrant:vagrant /etc/bind
      sudo chmod -R 755 /etc/bind
      
      
      sudo cp /vagrant/configs/named.conf.local.DNSB /etc/bind/named.conf.local
      
      
      sudo systemctl restart bind9
    SHELL
  end
end
