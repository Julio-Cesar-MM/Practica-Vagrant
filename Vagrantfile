VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.synced_folder "./html", "/var/www/html", SharedFoldersEnableSymlinksCreate: false

#Definimos el servidor 1
  config.vm.define "web1" do |web1|
    web1.vm.box = "ubuntu/jammy64"
    web1.vm.network "private_network", ip: "192.168.56.101"
    #web1.vm.network "forwarded_port", guest: 80, host: 8081
    web1.vm.hostname = "web1"
    web1.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end

    web1.vm.provision "file", source: "./html/index.html", destination: "/tmp/index.html"
    web1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
      systemctl enable apache2
    SHELL
  end

#Definimos el servidor 2
  config.vm.define "web2" do |web2|
    web2.vm.box = "ubuntu/jammy64"
    web2.vm.network "private_network", ip: "192.168.56.102"
    #web1.vm.network "forwarded_port", guest: 80, host: 8082
    web2.vm.hostname = "web2"
    web2.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end

    web2.vm.provision "file", source: "./html/index.html", destination: "/tmp/index.html"
    web2.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
      systemctl enable apache2
    SHELL
  end
end

