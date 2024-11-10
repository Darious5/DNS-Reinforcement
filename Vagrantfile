Vagrant.configure("2") do |config|
  # Configuración del servidor DNS Maestro (DNSA)
  config.vm.define "DNSA" do |dnsa|
    dnsa.vm.box = "debian/bookworm64"
    dnsa.vm.network "private_network", ip: "192.168.57.10"
    dnsa.vm.provision "shell", inline: <<-SHELL
      apt update && apt install -y bind9 dnsutils
    SHELL
    dnsa.vm.provision "file", source: "configs/named.conf.local.DNSA", destination: "/etc/bind/named.conf.local"
    dnsa.vm.provision "file", source: "configs/db.ies.test.informatica", destination: "/etc/bind/db.ies.test.informatica"
    dnsa.vm.provision "file", source: "configs/db.ies.test.aulas", destination: "/etc/bind/db.ies.test.aulas"
    dnsa.vm.provision "file", source: "configs/db.ies.test.departamentos", destination: "/etc/bind/db.ies.test.departamentos"
    dnsa.vm.provision "shell", inline: <<-SHELL
      systemctl restart bind9
    SHELL
  end

  # Configuración del servidor DNS Esclavo (DNSB)
  config.vm.define "DNSB" do |dnsb|
    dnsb.vm.box = "debian/bookworm64"
    dnsb.vm.network "private_network", ip: "192.168.57.11"
    dnsb.vm.provision "shell", inline: <<-SHELL
      apt update && apt install -y bind9 dnsutils
    SHELL
    dnsb.vm.provision "file", source: "configs/named.conf.local.DNSB", destination: "/etc/bind/named.conf.local"
    dnsb.vm.provision "shell", inline: <<-SHELL
      systemctl restart bind9
    SHELL
  end
end
