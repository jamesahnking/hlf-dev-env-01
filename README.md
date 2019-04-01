NEW REPO FOR DEV ENVIRO - OLD REPO DELETED

**For Local Development Enviroment  Set Up:** 
> <https://github.com/jamesahnking/hlf-dev-env-01/blob/master/HyperLedgerFabric_Dev_Environment_SetUp.md>

Once you have everything set up you can clone this repo and run vagrant up it will take care of everything. 
```
$ git clone git@github.com:jamesahnking/hlf-dev-env-01.git
$ cd hlf-dev-env-01.git 
$ vagrant up
```
If you get this error when working to connect using docker-machine

```
Checking connection to Docker...
Error creating machine: Error checking the host: Error checking and/or regenerating the certs: There was an error validating certificates for host "127.0.0.1:2376": dial tcp 127.0.0.1:2376: connect: connection refused
```

Add the following to your Vagrantfile

```
> config.vm.network "forwarded_port", guest: 2376, host: 2376
```

Vagrant commands
================
> vagrant up
> vagrant ssh
> vagrant halt
> vagrant destroy

Windows | Mac | Linux Docker
============================
+ DO NOT RUN DOCKER DAEMON on Host Machine
+ Install the Docker or Docker toolbox - Only docker client will be used
+ Make sure that following environment variables are NOT SET
  Use Control Panel on windows
  DOCKER_TLS
  DOCKER_TLS_VERIFY
+ Set the Environment following variable in Windows 
  DOCKER_HOST=tcp://localhost:2375

Install Vagrant
===============

Setup Ubuntu VM (~10 minutes first time)
========================================
+ Open a terminal window in the root of this folder
> vagrant up

Setup Vagrant Dev Environment (~5 min)
======================================
PS: If you get a permissions error, run this command
> chmod 755 ./scripts/*.sh

> Open a terminal window and cd to the root of this project

> vagrant up

> vagrant ssh

  $ ./scripts/install-prereqs.sh

// Logout of vagrant

  $ logout

> vagrant ssh

  $ ./scripts/install-fabric-tools.sh

  $ ./scripts/install-composer.sh

  

Download Fabric (~20 min)
=========================
Logout of Ubuntu
> vagrant ssh
  
  $ ./downloadFabric.sh

Validation
==========
You should be able to use the *docker* commands on your host machine
> set DOCKER_HOST=tcp://localhost:2375   
> unest DOCKER_TLS_VERIFY

Restart Machine**

You should be able to view docker images from the HOST machine 
