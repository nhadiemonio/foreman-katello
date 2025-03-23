Vagrant.configure("2") do |config|
  config.vm.define :foreman do |foreman|
    foreman.vm.box = "centos/stream9"
    foreman.vm.box_version = "20250320.0"
    foreman.vm.hostname = "foreman.my.local"
    foreman.vm.provider "virtualbox" do |vbox|
      vbox.name = "foreman"
      vbox.memory = 8192
      vbox.cpus = 4
    end
    foreman.vm.network "private_network", :ip => "192.168.56.200", :name => "VirtualBox Host-Only Ethernet Adapter", :adapter => 2
    foreman.vm.provision "file", source: "~/.ssh/id_ed25519.pub", destination: "/tmp/id_ed25519.pub"
    foreman.vm.provision "shell", inline: <<-SHELL
      cat /tmp/id_ed25519.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end
  config.vm.define :centos do |centos|
    centos.vm.box = "centos/stream9"
    centos.vm.box_version = "20250320.0"
    centos.vm.hostname = "centos.my.local"
    centos.vm.provider "virtualbox" do |vbox|
      vbox.name = "centos"
      vbox.memory = 2048
      vbox.cpus = 2
    end
    centos.vm.network "private_network", :ip => "192.168.56.10", :name => "VirtualBox Host-Only Ethernet Adapter", :adapter => 2
    centos.vm.provision "file", source: "~/.ssh/id_ed25519.pub", destination: "/tmp/id_ed25519.pub"
    centos.vm.provision "shell", inline: <<-SHELL
      cat /tmp/id_ed25519.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end
end