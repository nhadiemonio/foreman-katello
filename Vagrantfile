Vagrant.configure("2") do |config|
  config.vm.define :centos do |foreman|
    foreman.vm.box = "centos/stream9"
    foreman.vm.box_version = "20250320.0"
    foreman.vm.hostname = "foreman.my.local"
    foreman.vm.provider "virtualbox" do |vbox|
      vbox.name = "foreman"
      vbox.memory = 2048
      vbox.cpus = 2
    end
    foreman.vm.network "private_network", :ip => "192.168.56.200", :name => "VirtualBox Host-Only Ethernet Adapter", :adapter => 2
    foreman.vm.provision "file", source: "~/.ssh/id_ed25519.pub", destination: "/tmp/id_ed25519.pub"
    foreman.vm.provision "shell", inline: <<-SHELL
      cat /tmp/id_ed25519.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end
end