
Vagrant::configure("2") do |config|
  config.vm.box = "box-cutter/ubuntu1404-desktop"

  
  # Configure Selenium Grid
  config.vm.define :'selenium-grid' do |selenium_grid|
    selenium_grid.vm.box = "ubuntu/trusty64"
    selenium_grid.vm.provider "virtualbox" do |v|
      v.gui = false
    end
    selenium_grid.vm.network :private_network, ip: "192.168.10.10"
        selenium_grid.vm.hostname = "selenium.local.vm"
        selenium_grid.vm.provider :virtualbox do |vb|
          vb.customize [
                        "modifyvm", :id,
                        "--name", "selenium-grid",
                        "--memory", "1024",
                        "--cpus", 1,
                        "--natdnshostresolver1", "on",
                        "--natdnsproxy1", "on"
                       ]
        end
  end

    # Configure Selenium Node
  config.vm.define :'node1' do |grid_node|
    grid_node.vm.box = "box-cutter/ubuntu1404-desktop"
    grid_node.vm.provider "virtualbox" do |v|
      v.gui = false
    end
    grid_node.vm.network :private_network, ip: "192.168.10.11"
        grid_node.vm.hostname = "node.selenium.vm"
        grid_node.vm.provider :virtualbox do |vb|
          vb.customize [
                        "modifyvm", :id,
                        "--name", "node1",
                        "--memory", "1024",
                        "--cpus", 1,
                        "--natdnshostresolver1", "on",
                        "--natdnsproxy1", "on"
                       ]
        end
  end
end
