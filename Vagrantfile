Vagrant.configure("2") do |config|
  config.vm.define "indexer" do |indexer|
    indexer.vm.box = "generic/ubuntu2204"
    indexer.vm.network "private_network", ip: "192.168.56.10"
    indexer.vm.hostname = "indexer"

    indexer.vm.provider "virtualbox" do |vb|
        vb.cpus = "2"
        vb.memory = "4096"
    end

    indexer.vm.synced_folder "./shared/", "/vagrant"
    indexer.vm.provision "shell", inline: <<-SHELL
        apt update
        apt install curl -y
        rm -rf /wazuh-setup && mkdir /wazuh-setup && cd /wazuh-setup
        curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
        cp /vagrant/config.yml /wazuh-setup/
        bash wazuh-install.sh --generate-config-files
        rm -f /vagrant/*.tar
        cp wazuh-install-files.tar /vagrant
        bash wazuh-install.sh -o --wazuh-indexer node-1
        bash wazuh-install.sh --start-cluster
    SHELL
  end

  config.vm.define "server" do |server|
    server.vm.box = "generic/ubuntu2204"
    server.vm.network "private_network", ip: "192.168.56.20"
    server.vm.hostname = "server"

    server.vm.provider "virtualbox" do |vb|
        vb.cpus = "2"
        vb.memory = "4096"
    end

    server.vm.synced_folder "./shared/", "/vagrant"
    server.vm.provision "shell", inline: <<-SHELL
        apt update
        apt install curl -y
        rm -rf /wazuh-setup && mkdir /wazuh-setup && cd /wazuh-setup
        curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
        cp /vagrant/wazuh-install-files.tar /wazuh-setup
        bash wazuh-install.sh -o --wazuh-server wazuh-1
    SHELL
  end

  config.vm.define "dashboard" do |dashboard|
    dashboard.vm.box = "generic/ubuntu2204"
    dashboard.vm.network "private_network", ip: "192.168.56.30"
    dashboard.vm.hostname = "dashboard"

    dashboard.vm.provider "virtualbox" do |vb|
        vb.cpus = "2"
        vb.memory = "4096"
    end

    dashboard.vm.synced_folder "./shared/", "/vagrant"
    dashboard.vm.provision "shell", inline: <<-SHELL
        apt update
        apt install curl -y
        rm -rf /wazuh-setup && mkdir /wazuh-setup && cd /wazuh-setup
        curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
        cp /vagrant/wazuh-install-files.tar /wazuh-setup
        bash wazuh-install.sh -o --wazuh-dashboard dashboard
    SHELL
  end
end
