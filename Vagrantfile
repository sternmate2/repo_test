

#################################################################################################### node1 ##############################################################

Vagrant.configure(2) do |config|
  config.vm.define "node1" do |node1|
    node1.vm.box = "ubuntu/trusty64"
    node1.vm.hostname = "node1"
    node1.vm.network "private_network", ip: "192.168.33.10"
#    node1.vm.provision "shell", inline: "sudo chown vagrant:vagrant /home/vagrant/.ssh/"
  end


#################################################################################################### node 2 ##############################################################

  config.vm.define "node2" do |node2|
    node2.vm.box = "ubuntu/trusty64"
    node2.vm.hostname = "node2"
    node2.vm.network "private_network", ip: "192.168.33.20"

  end  


#################################################################################################### node 3 ##############################################################

  config.vm.define "node3" do |node3|
    node3.vm.box = "ubuntu/trusty64"
    node3.vm.hostname = "node3"
    node3.vm.network "private_network", ip: "192.168.33.30"
  end


#################################################################################################### node 4 ##############################################################

  config.vm.define "node4" do |node4|
    node4.vm.box = "ubuntu/trusty64"
    node4.vm.hostname = "node4"
    node4.vm.network "private_network", ip: "192.168.33.40"
  end


#################################################################################################### node 5 ##############################################################


  config.vm.define "node5" do |node5|
    node5.vm.box = "ubuntu/trusty64"
    node5.vm.hostname = "node5"
    node5.vm.network "private_network", ip: "192.168.33.50"
  end





############################################### master #######################################

  config.vm.box = "bento/centos-7.3"
  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.33.11"
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/init.yml"
      file.destination = "/home/vagrant/ansible/init.yml"
    end

################################## install.ansible - change.permmision - copy.hosts.file #####

    master.vm.provision :file do |file|
      file.source = "~/.ssh/id_rsa.pub"
      file.destination = "~/.ssh/id_rsa.pub"
    end
    master.vm.provision :file do |file|
      file.source = "~/.ssh/id_rsa"
      file.destination = "~/.ssh/id_rsa"
    end
    master.vm.provision "shell", inline: <<-SHELL
      yum install -y ansible
      sudo chown vagrant:vagrant /etc/ansible/hosts
      sudo chown vagrant:vagrant /home/vagrant/.ssh/authorized_keys
    SHELL
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/host"
      file.destination = "/etc/ansible/hosts"
    end
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/ansible.cfg"
      file.destination = "/home/vagrant/ansible/ansible.cfg"
    end
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/init.yml"
      file.destination = "/home/vagrant/ansible/init.yml"
    end
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/node.conf"
      file.destination = "/home/vagrant/ansible/node.conf"
    end
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/blue.conf"
      file.destination = "/home/vagrant/ansible/blue.conf"
    end

    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/yellow.conf"
      file.destination = "/home/vagrant/ansible/yellow.conf"
    end
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/inx"
      file.destination = "/home/vagrant/ansible/inx"

    end
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/test.html"
      file.destination = "/home/vagrant/ansible/test.html"
    end
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/blue.html"
      file.destination = "/home/vagrant/ansible/blue.html"
    end

    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/yellow.html"
      file.destination = "/home/vagrant/ansible/yellow.html"
    end
    master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/jenkins"
      file.destination = "/home/vagrant/ansible/roles/jenkins/tasks/main.yml"
    end
     master.vm.provision :file do |file|
      file.source = "/root/vag/ansible-machines/test/git"
      file.destination = "/home/vagrant/ansible/roles/git/tasks/main.yml"
    end

    master.ssh.forward_agent = true
    master.ssh.insert_key = false
    master.vm.provision "shell", inline: <<-SHELL
      sudo chown vagrant:vagrant /home/vagrant/ansible/test.html
      sudo chmod 777 /home/vagrant/ansible/test.html
      sudo chown vagrant:vagrant /home/vagrant/ansible/blue.html
      sudo chmod 777 /home/vagrant/ansible/blue.html
      sudo chown vagrant:vagrant /home/vagrant/ansible/yellow.html
      sudo chmod 777 /home/vagrant/ansible/yellow.html
      cd /home/vagrant/ansible/
      ansible-playbook init.yml
    SHELL

  end
end
