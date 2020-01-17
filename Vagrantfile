Vagrant.configure("2") do |config|
    centos_box = "bento/centos-7"
    net_ip = "192.168.50"

  config.vm.define :ansible, primary: true do |ansible_config|
    ansible_config.vm.provider "virtualbox" do |vb|
      vb.name = "ansible"
      vb.memory = "2048"
      vb.cpus = 1
  
    end

    ansible_config.vm.box = "#{centos_box}"
    ansible_config.vm.host_name = "ansible.local"
    ansible_config.vm.network "private_network", ip: "#{net_ip}.10"
    ansible_config.vm.synced_folder ".", "/vagrant", disabled: true
    ansible_config.vm.provision :shell, path: "scripts/ansible.sh"
    ansible_config.ssh.insert_key = false
    ansible_config.ssh.private_key_path = ["keys/id_rsa", "~/.vagrant.d/insecure_private_key"]
    ansible_config.vm.provision "file", source: "keys/id_rsa.pub", destination: "~/.ssh/authorized_keys"
    ansible_config.vm.provision "file", source: "keys/id_rsa", destination: "~/.ssh/id_rsa"
    ansible_config.vm.provision "file", source: "keys/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
    ansible_config.vm.synced_folder "data/ansible", "/home/vagrant/ansible", type: "virtualbox"
    ansible_config.vm.synced_folder "data/gitlab", "/home/vagrant/gitlab", type: "virtualbox"
 
  end

  config.vm.define :minion do |minion_config|
      minion_config.vm.provider "virtualbox" do |vb|
        vb.name = "minion"
        vb.memory = "1048"
        vb.cpus = 1
      end

      minion_config.vm.box = "#{centos_box}"
      minion_config.vm.hostname = "minion.valocal"
      minion_config.vm.network "private_network", ip: "#{net_ip}.11"
      minion_config.vm.synced_folder ".", "/vagrant", disabled: true
      minion_config.ssh.insert_key = false
      minion_config.ssh.private_key_path = ["keys/id_rsa", "~/.vagrant.d/insecure_private_key"]
      minion_config.vm.provision "file", source: "keys/id_rsa.pub", destination: "~/.ssh/authorized_keys"
    
      
  end

end
