Vagrant.configure("2") do |config|
  config.vm.define :foreman do |foreman|
    foreman.vm.box = "bento/centos-stream-9"
    foreman.vm.box_version = "202502.21.0"
    foreman.vm.hostname = "foreman.my.local"
    foreman.vm.synced_folder ".", "/vagrant", disabled: true
    foreman.vm.provider "virtualbox" do |vbox|
      vbox.name = "foreman"
      vbox.memory = 32768
      vbox.cpus = 8
    end
    foreman.vm.network "private_network", :ip => "192.168.56.200", :name => "vboxnet0", :adapter => 2
    foreman.vm.provision "file", source: "~/.ssh/id_ed25519.pub", destination: "/tmp/id_ed25519.pub"
    foreman.vm.provision "file", source: "foreman-install", destination: "/tmp/foreman-install"
    foreman.vm.provision "shell", inline: <<-SHELL
      cat /tmp/id_ed25519.pub >> /home/vagrant/.ssh/authorized_keys
      sudo dnf update -y
      sudo dnf install python3.12 python3.12-pip -y
      sudo python3.12 -m pip install ansible ansible-core --upgrade
    SHELL
    foreman.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/tmp/foreman-install/build.yml"
      ansible.verbose = true
    end
  end
  config.vm.define :centos do |centos|
    centos.vm.box = "bento/centos-stream-9"
    centos.vm.box_version = "202502.21.0"
    centos.vm.hostname = "centos.my.local"
    centos.vm.synced_folder ".", "/vagrant", disabled: true
    centos.vm.provider "virtualbox" do |vbox|
      vbox.name = "centos"
      vbox.memory = 2048
      vbox.cpus = 2
    end
    centos.vm.network "private_network", :ip => "192.168.56.200", :name => "vboxnet0", :adapter => 2
    centos.vm.provision "file", source: "~/.ssh/id_ed25519.pub", destination: "/tmp/id_ed25519.pub"
    centos.vm.provision "shell", inline: <<-SHELL
      cat /tmp/id_ed25519.pub >> /home/vagrant/.ssh/authorized_keys
      sudo dnf update -y
      sudo dnf install python3.12 python3.12-pip -y
      sudo python3.12 -m pip install ansible ansible-core --upgrade
    SHELL
  end
end
