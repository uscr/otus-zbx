zabbix_vmname = "zabbix"
web_vmname = "web"
ansible_vmname = "ansible"

zabbix_memory = 512
web_memory = 512
ansible_memory = 512

zabbix_cpu = 2
web_cpu = 1
ansible_cpu = 1

ubuntu_box = "bento/ubuntu-22.04"

$script = <<-'SCRIPT'
sudo apt -y install sshpass
sudo pip3 install PyMySQL
sudo pip3 install zabbix-api
ansible-galaxy collection install -r /otus/requirements.yml
ansible-galaxy role install -r /otus/requirements.yml
ansible-playbook -i /otus/otus.inv /otus/zabbix.yml
ansible-playbook -i /otus/otus.inv /otus/wordpress-lamp_ubuntu1804/playbook.yml
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.define zabbix_vmname do |subconfig|
    subconfig.vm.synced_folder "./", "/otus", type: 'virtualbox'
    subconfig.vm.box = ubuntu_box
    subconfig.vm.hostname = zabbix_vmname
    subconfig.vm.network :private_network, ip: "192.168.50.11" 
    subconfig.vm.provider "virtualbox" do |vb|
      vb.memory = zabbix_memory
      vb.cpus = zabbix_cpu
    end
  end
  config.vm.define web_vmname do |subconfig|
    subconfig.vm.synced_folder "./", "/otus", type: 'virtualbox'
    subconfig.vm.box = ubuntu_box
    subconfig.vm.hostname = web_vmname
    subconfig.vm.network :private_network, ip: "192.168.50.12" 
    subconfig.vm.provider "virtualbox" do |vb|
      vb.memory = web_memory
      vb.cpus = web_cpu
    end
  end  
  config.vm.define ansible_vmname do |subconfig|
    subconfig.vm.synced_folder "./", "/otus", type: 'virtualbox'
    subconfig.vm.box = "mrg/ansible"
    subconfig.vm.hostname = ansible_vmname
    subconfig.vm.network :private_network, ip: "192.168.50.13" 
    subconfig.vm.provider "virtualbox" do |vb|
      vb.memory = ansible_memory
      vb.cpus = ansible_cpu
    end
    subconfig.vm.provision "shell", inline: $script
  end

end

