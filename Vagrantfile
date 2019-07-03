VAGRANTFILE_API_VERSION = "2"
BASE_HOSTNAME= "vm"
BASE_IP = "10.0.0."
NUM_MACHINES = 3
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  (0..NUM_MACHINES-1).each do |id|
    config.vm.define "vm#{id}" do |machine|
      machine.vm.box="centos/7"
      machine.vm.hostname = "#{BASE_HOSTNAME}#{id}"
      machine.vm.network "private_network", ip: "#{BASE_IP}#{2+id}"
      machine.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--memory", 512]
        v.customize ["modifyvm", :id, "--name", "#{BASE_HOSTNAME}#{id}"]
        v.customize ["modifyvm", :id, "--ioapic", "on"]
        v.customize ["modifyvm", :id, "--cpus", 1]
      end
      machine.ssh.insert_key = false
      if id == NUM_MACHINES
        machine.vm.provision :shell, inline: "echo Good job"
      end
    end
  end
end

