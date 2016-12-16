# -*- mode: ruby -*-
# vi: set ft=ruby :


$prepare_system = <<SCRIPT

cat >/etc/yum.repos.d/docker.repo <<-EOF
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/oraclelinux/7
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF

yum -y install docker-engine
systemctl start docker.service
usermod -aG docker vagrant
systemctl enable docker.service

mkdir -p /etc/systemd/system/docker.service.d/ && tee /etc/systemd/system/docker.service.d/docker.conf << EOF
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -D -H tcp://0.0.0.0:2375 -H unix://
EOF

systemctl daemon-reload && systemctl restart docker

# Don't know why, by interface is down on guest when 'vboxmanage list hostonlyifs' reports it's up !
ifup enp0s8

SCRIPT



Vagrant.configure("2") do |config|
  config.vm.box = "boxcutter/ol72"
  
  config.vm.provision :shell, :inline => "sudo yum -y update"
  config.vm.provision :shell, :inline => "sudo yum -y update"
  config.vm.provision :reload
  config.vm.provision :shell, :inline => $prepare_system


  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
    vb.customize ['modifyvm', :id, '--cableconnected1', 'on']
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vbguest.auto_update = false  

  config.vm.define "swarm-1" do |config|
    config.vm.hostname = "swarm-1"
    config.vm.network "private_network", ip: "10.0.7.11"
  end

  config.vm.define "swarm-2" do |config|
    config.vm.hostname = "swarm-2"
    config.vm.network "private_network", ip: "10.0.7.12"
  end

  config.vm.define "swarm-3" do |config|
    config.vm.hostname = "swarm-3"
    config.vm.network "private_network", ip: "10.0.7.13"
  end

end
