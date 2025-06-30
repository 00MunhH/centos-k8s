# -*- mode: ruby -*-
# vi: set ft=ruby :
# vagrant files for k8s cluster(one master node, two worker nodes)
# edited by lee

VAGRANTFILE_API_VERSION = "2"

NODES = {
  master: "master",
  worker1: "worker1",
  worker2: "worker2"
}

IPS = {
  NODES[:worker1] => "192.168.73.20",
  NODES[:worker2] => "192.168.73.30",
  NODES[:master] => "192.168.73.10"
}

k8s_cluster = {
  NODES[:worker1] => { :ip => IPS[NODES[:worker1]], :cpus => 1, :memory => 3072 },
  NODES[:worker2] => { :ip => IPS[NODES[:worker2]], :cpus => 1, :memory => 3072 },
	NODES[:master]=> { :ip => IPS[NODES[:master]], :cpus => 2, :memory => 4096 }
}

host_entries = IPS.map { |name, ip| "#{ip} #{name}" }.join("\n") + "\n"
File.write("hosts.env", host_entries)

 
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  k8s_cluster.each do |hostname, info|

    config.vm.define hostname do |cfg|
      cfg.vm.provision "file", source: "hosts.env", destination: "/tmp/hosts.env"

      cfg.vm.provider "virtualbox" do |vb,override|
        config.vm.box = "generic/centos9s"
        override.vm.network "private_network", ip: "#{info[:ip]}"
        override.vm.host_name = hostname
        vb.name = hostname
				vb.gui = false
        vb.customize ["modifyvm", :id, "--memory", info[:memory], "--cpus", info[:cpus]]
				if hostname == NODES[:master] then
					override.vm.provision "shell", path: "ssh_conf.sh", privileged: true
					override.vm.provision "shell", path: "install_cluster.sh", privileged: true
					override.vm.provision "shell", path: "run_in_master.sh", privileged: true
					override.vm.provision "shell", path: "account.sh", privileged: false
					override.vm.provision "shell", path: "send_pub_key.sh", privileged: false
				else
					override.vm.provision "shell", path: "ssh_conf.sh", privileged: true
					override.vm.provision "shell", path: "install_cluster.sh", privileged: true
				end  
      end  
    end  
  end  
end 

