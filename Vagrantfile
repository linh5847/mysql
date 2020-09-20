NET = "192.168.132"
DOMAIN = ".vntechsol.com"


Vagrant.configure("2") do |config|
  
  vm = 2
  (1..vm).each do |machine_id|
    config.vm.define "mysql-node#{machine_id}" do |machine|
      machine.vm.hostname = "mysql-node#{machine_id}" + DOMAIN
      machine.vm.box = "centos/7"
      machine.ssh.insert_key = false
      machine.vm.network "forwarded_port", guest: 22, host: "227#{machine_id}"
      machine.ssh.port = "227#{machine_id}"
      machine.vm.network "forwarded_port", guest: 3306, host: "333#{machine_id}"
      machine.vm.network "private_network", ip: NET + ".3#{machine_id}"
      machine.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=755", "fmode=644"]
      machine.vm.boot_timeout = 60

      machine.vm.provider "virtualbox" do |vm|
        vm.cpus = 2
        vm.memory = 1024
        vm.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
      end

      if machine_id == vm
        machine.vm.provision "ansible_local" do |ansible|
          ansible.limit = "all"
          ansible.verbose = true
          ansible.become = true
          ansible.raw_arguments = ["-v"]
          ansible.playbook = "site.yml"
          ansible.tags = ["mysql_master_slave"]
          ansible.inventory_path = "inventory.ini"
          ansible.extra_vars = {
            ansible_ssh_users: 'vagrant'
          }
          ansible.groups = {
            "mysql_master" => ["mysql-node1"],
            "mysql_slave" => ["mysql-node2"]
          }
        end
      end
    end
  end
end
