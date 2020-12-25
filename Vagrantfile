# -*- mode: ruby -*-
# vi: set ft=ruby :


# Hosts definition
planets = {
  "mercury" => { :ip => "10.0.0.3" },
  "venus" => { :ip => "10.0.0.4" },
  "earth" => { :ip => "10.0.0.5" }
}

# Provisioning scripts
$sun_provision = <<-'SCRIPT'
yum install -y epel-release 
yum makecache
yum install -y ansible
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "centos/8"

  config.vm.define "sun", primary: true do |host|
    host.vm.hostname = "sun"
    host.vm.network "private_network", ip: "10.0.0.2"
    host.vm.synced_folder "./sun/", "/vagrant", type: "virtualbox"
    host.vm.provision "shell", inline: $sun_provision
  end

  # Iterate over planets array
  planets.each_with_index do |(hostname, info), index|
    config.vm.define hostname do |cfg|
      cfg.vm.network :private_network, ip: "#{info[:ip]}"
      cfg.vm.hostname = hostname
      #config.vm.provider.vb.name = hostname
      cfg.vm.synced_folder "./planet/", "/vagrant", type: "virtualbox"
    end
  end



end


