
Vagrant::configure("2") do |config|

  # Configure Selenium Hub
  config.vm.define :'hub' do |hub|
    hub.vm.box = "ubuntu/trusty64"
    hub.vm.provider "virtualbox" do |v|
      v.gui = false
    end
    hub.vm.network :private_network, ip: "192.168.10.10"
        hub.vm.hostname = "hub.selenium.vm"
        hub.vm.provider :virtualbox do |vb|
          vb.customize [
                        "modifyvm", :id,
                        "--name", "selenium-hub",
                        "--memory", "1024",
                        "--cpus", 1,
                        "--natdnshostresolver1", "on",
                        "--natdnsproxy1", "on"
                       ]
        end
  end

  # Configure Selenium Node
  config.vm.define :'node1' do |node|
    node.vm.box = "box-cutter/ubuntu1404-desktop"
    node.vm.provider "virtualbox" do |v|
      v.gui = true
    end

    node.vm.network :private_network, ip: "192.168.10.11"
        node.vm.hostname = "node1.selenium.vm"
        node.vm.provider :virtualbox do |vb|
          vb.customize [
                        "modifyvm", :id,
                        "--name", "selenium-node1",
                        "--memory", "1024",
                        "--cpus", 1,
                        "--natdnshostresolver1", "on",
                        "--natdnsproxy1", "on"
                       ]
        end

    # hack to get vagrant to provision all machines at once
    node.vm.provision "ansible" do |ansible|
      ansible.groups = {
        "hubs" => ["hub"],
        "nodes" => ["node1", "node2", "node3"]
      }
      ansible.playbook = "provisioning/playbook.yml"
      ansible.limit = 'all'
      ansible.sudo = true
    end

  end

end
