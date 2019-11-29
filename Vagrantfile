$hosts_script = <<SCRIPT
apt-get update
apt-get -q -y install python
git clone https://github.com/guidolarrain1981/docker-redis.git
SCRIPT

$hosts_script_2 = <<SCRIPT
apt-get update
apt-get -q -y install redis-tools
echo "#######################################"
echo "#######################################"
echo "###### Get Cluster Info ###############"
echo "#######################################"
echo "#######################################"
redis-cli -a password INFO 
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.hostname = "redis-cluster"
  config.vm.define "redis-cluster"
  config.vm.provider :virtualbox do |v|
    v.name = "redis"
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end
  config.vm.network :private_network, ip: "10.211.55.106"
  config.vm.provision :shell, :inline => $hosts_script

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "ansible/site.yml"
    ansible.inventory_path = "ansible/hosts"
  end

  config.vm.provision :shell, :inline => $hosts_script_2

end
