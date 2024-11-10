Vagrant.configure("2") do |config|
  # Configuración del servidor DNS Maestro
  config.vm.define "DNSA" do |dnsa|
    dnsa.vm.box = "debian/bookworm64"
    dnsa.vm.network "private_network", ip: "192.168.57.10"
    dnsa.vm.provision "shell", inline: <<-SHELL
      apt update && apt install -y bind9 dnsutils
    SHELL
  end

  # Configuración del servidor DNS Esclavo
  config.vm.define "DNSB" do |dnsb|
    dnsb.vm.box = "debian/bookworm64"
    dnsb.vm.network "private_network", ip: "192.168.57.11"
    dnsb.vm.provision "shell", inline: <<-SHELL
      apt update && apt install -y bind9 dnsutils
    SHELL
  end
end