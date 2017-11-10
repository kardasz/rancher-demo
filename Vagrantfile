# -*- mode: ruby -*-
# vi: set ft=ruby :
box      = 'debian/contrib-stretch64'

# Rancher VM configuration
rancher_hostname = 'rancher.docker'
rancher_ip       = '172.12.12.10'
rancher_ram      = '1024'
rancher_cpus     = 2
rancher_pae      = 'on'

# VM configuration
vm1_hostname = 'rancher-vm-1.docker'
vm1_ip       = '172.12.12.11'
vm1_ram      = '1024'
vm1_cpus     = 2
vm1_pae      = 'on'

vm2_hostname = 'rancher-vm-2.docker'
vm2_ip       = '172.12.12.12'
vm2_ram      = '1024'
vm2_cpus     = 2
vm2_pae      = 'on'

Vagrant.require_version ">= 1.9.1"

Vagrant.configure("2") do |config|
  config.vm.box = box
  config.ssh.forward_agent = true

  config.vm.define 'rancher' do |rancher|
      rancher.vm.provider "virtualbox" do |v|
          v.customize [
              "modifyvm", :id,
              "--name", rancher_hostname,
              "--memory", rancher_ram,
              "--cpus", rancher_cpus,
              "--pae", rancher_pae
          ]
      end

      rancher.vm.network "private_network", ip: rancher_ip, :netmask => "255.255.255.0"
      rancher.vm.hostname = rancher_hostname

      rancher.vm.provision "setup", type: "shell", privileged: true, inline: <<-SHELL
        export DEBIAN_FRONTEND=noninteractive
        echo 'deb http://ftp.debian.org/debian stretch-backports main contrib non-free' > /etc/apt/sources.list.d/stretch-backports.list
        apt-get update
        apt-get install -y make vim wget htop screen rsync curl git bash-completion apt-transport-https ca-certificates software-properties-common
        curl https://releases.rancher.com/install-docker/17.06.sh | sh
        curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
        chmod +x /usr/local/bin/docker-compose
        usermod -a -G docker,www-data vagrant
        service docker restart
        docker pull rancher/server
      SHELL
  end

  config.vm.define 'vm1' do |node|
      node.vm.provider "virtualbox" do |v|
          v.customize [
              "modifyvm", :id,
              "--name", vm1_hostname,
              "--memory", vm1_ram,
              "--cpus", vm1_cpus,
              "--pae", vm1_pae
          ]
      end

      node.vm.network "private_network", ip: vm1_ip, :netmask => "255.255.255.0"
      node.vm.hostname = vm1_hostname

      node.vm.provision "setup", type: "shell", privileged: true, inline: <<-SHELL
        export DEBIAN_FRONTEND=noninteractive
        echo 'deb http://ftp.debian.org/debian stretch-backports main contrib non-free' > /etc/apt/sources.list.d/stretch-backports.list
        apt-get update
        apt-get install -y make vim wget htop screen rsync curl git bash-completion apt-transport-https ca-certificates software-properties-common
        curl https://releases.rancher.com/install-docker/17.06.sh | sh
        curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
        chmod +x /usr/local/bin/docker-compose
        usermod -a -G docker,www-data vagrant
        service docker restart
      SHELL
  end

  config.vm.define 'vm2' do |node|
      node.vm.provider "virtualbox" do |v|
          v.customize [
              "modifyvm", :id,
              "--name", vm2_hostname,
              "--memory", vm2_ram,
              "--cpus", vm2_cpus,
              "--pae", vm2_pae
          ]
      end

      node.vm.network "private_network", ip: vm2_ip, :netmask => "255.255.255.0"
      node.vm.hostname = vm2_hostname

      node.vm.provision "setup", type: "shell", privileged: true, inline: <<-SHELL
        export DEBIAN_FRONTEND=noninteractive
        echo 'deb http://ftp.debian.org/debian stretch-backports main contrib non-free' > /etc/apt/sources.list.d/stretch-backports.list
        apt-get update
        apt-get install -y make vim wget htop screen rsync curl git bash-completion apt-transport-https ca-certificates software-properties-common
        curl https://releases.rancher.com/install-docker/17.06.sh | sh
        curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
        chmod +x /usr/local/bin/docker-compose
        usermod -a -G docker,www-data vagrant
        service docker restart
      SHELL
  end
end
