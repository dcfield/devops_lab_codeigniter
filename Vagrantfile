Vagrant.configure("2") do |config|

  # Vagrant box we will use for all our Virtual Machines
  config.vm.box = "bento/centos-7.5"

  # VM to act as the client application
  config.vm.define "client", primary: true do |client|
    client.vm.hostname="client"
    client.vm.network "private_network", ip: "192.168.33.10"
  end

  # VM for our apache server
  config.vm.define "web" do |web|
    web.vm.hostname="apache"
    web.vm.network "private_network", ip: "192.168.33.20"
    web.vm.provision "ansible" do |ansible|
      ansible.playbook="application.yml"
    end
  end

  # VM for our integration / development server
  config.vm.define "webdev" do |web|
    web.vm.hostname="apache"
    web.vm.network "private_network", ip: "192.168.33.25"
    web.vm.provision "ansible" do |ansible|
      ansible.playbook="application.yml"
    end
  end

  # VM for our database
  config.vm.define "db" do |db|
    db.vm.hostname = "mysql"
    db.vm.network "private_network", ip: "192.168.33.30"
    db.vm.provision "ansible" do |ansible|
      ansible.playbook="database.yml"
    end
  end

  # VM for our Jenkins machine
  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.box = "bento/ubuntu-18.04"
    jenkins.vm.hostname = "jenkins"
    jenkins.vm.network "private_network", ip: "192.168.33.40"
    jenkins.vm.provision "ansible" do |ansible|
      ansible.playbook = "jenkins.yml"
    end
  end

  # config.vm.provision "shell", inline: "sudo yum update -y"
end

