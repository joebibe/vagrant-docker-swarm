servers=[
  {
    :hostname => "manager",
    :ip => "172.28.128.9",
    :box => "debian/stretch64",
    :ram => 512,
    :cpu => 1
  },
  {
    :hostname => "worker-1",
    :ip => "172.28.128.10",
    :box => "debian/stretch64",
    :ram => 512,
    :cpu => 1
  },
  {
    :hostname => "worker-2",
    :ip => "172.28.128.11",
    :box => "debian/stretch64",
    :ram => 512,
    :cpu => 1
  }
]
Vagrant.configure(2) do |config|
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      node.vm.network "private_network", ip: machine[:ip]
      if machine[:hostname] == "manager"
        node.vm.provision "docker",
          images: ["joebibe/vagrant-docker-swarm"]
      else
        node.vm.provision "docker"
      end
      node.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
        vb.customize ["modifyvm", :id, "--name", machine[:hostname]]
      end
    end
  end
end
