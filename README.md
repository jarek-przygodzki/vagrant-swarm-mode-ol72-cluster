# Vagrant Swarm mode cluster

Run a Swarm  mode cluster locally using Vagrant.

# Requirements 

Install [Vagrant][vagranthome] with [reload][vagrant-reload] plugin and [Docker][dockerhome] on your machine.

Ensure you have a valid [Vagrant provider][vagrantprovider] installed.

# Setup

## Boot Vagrant machines

The first thing you must do is to start the Vagrant machines using your favorite provider:

```
$ git clone git@github.com:jarek-przygodzki/vagrant-swarm-mode-ol72-cluster.git
$ cd vagrant-swarm-mode-ol72-cluster
$ vagrant up --provider virtualbox
```

Supported providers:

* virtualbox

## Bootstrap script

If you're on *nix, you can execute the `start_cluster.sh` script to bootstrap the Swarm cluster:

```shell
$ chmod +x start_cluster.sh
$ ./start_cluster.sh
```

## Commands

Or execute the following commands to start the cluster.

TODO

[vagranthome]: https://www.vagrantup.com/docs/installation/  "Vagrant installation"
[vagrantprovider]: https://www.vagrantup.com/docs/providers/ "Vagrant providers"
[dockerhome]: https://docs.docker.com/engine/installation/  "Docker installation"
[vagrant-reload]: https://github.com/aidanns/vagrant-reload "Vagrant Reload Provisioner"

