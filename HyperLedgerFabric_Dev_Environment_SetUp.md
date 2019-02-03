# Hyperledger Local Environment setup - Mixed Mode

## Mixed Mode Explained

- `Hyperledger Fabric` installed on `VM`

- Virtualization handled by `Virtualbox`

- VM Creation & Management by `Vagrant`


`Hyperledger Composer` should be installed on the Host `Machine`
The `Host` will communicate with the `VM` using Hyperledgers `docker-machine`

> <https://www.udemy.com/hyperledger-fabric-composer-first-practical-blockchain/learn/v4/content>

> <https://hyperledger.github.io/composer/latest/installing/installing-prereqs.html#macos>

---

## Project setup and Git configuration for Vagrant VM

Create project folder

>`mkdir ~/ProjectFolder && cd ~/ProjectFolder`

Initilalize your Git inside of `ProjectFolder`.

>`git init`

Check `git` status:

> `git status`

**Add** files and **track**

> `git add <filename>`

 **Commit** files:

> `git commit -m "Message or note"`

- To view **History**

> `git log`

- To rollback a version and **checkout** a previeous **commit** 

> `git checkout 1234567`

- Note: this will create a `'detached HEAD'` state

- A `'detached HEAD'` allows make changes but it wont effect any branches if you do another checkout.

- To create a new **branch** that is not `detached`:  

> `git checkout -b 'newBranchNameHere'`

- To add multiple files at once: 

> `git add -A`
---

## Set up your `SSH` key for Github

- Create key using your github account email

> `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

- This will create a new rsa key pair

> `Generating public/private rsa key pair.`

- When prompted press Enter: (This excepts the default file location)

>`Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]`

- When prompted to enter a passphrase create one(it will ask twice)

> `Enter passphrase (empty for no passphrase): [Type a passphrase]`

- Add key to **`SSH agent`**:

> `/usr/bin/ssh-add -K ~/.ssh/id_rsa`

- Copy new key from terminal with

> `pbcopy < ~/.ssh/id_rsa.pub`

- Go to your GitHub account `Settings/SSH and GPG Keys` and paste key in `New SSH Key field`

### CLI remote repository push and pull

- Create New Repo on Github

- **Add** existing repo:

> `git remote add origin git@github.com:jamesahnking/nameOfRepositoryHere.git`

- **Push** repo to remote repository:

> `git push -u origin master`

---

## 1. Install Vagrant

Vagrant is a tool for building and managing virtual machine environments in a single workflow.

> <https://www.vagrantup.com/intro/getting-started/index.html>

- Check version

>`vagrant version`

- Install Vagrant

> `brew cask install vagrant`

- Vagrant upgrade

> `brew cask upgrade vagrant`

## 2. Install Virtualbox

Oracle VM VirtualBox is a lightweight application that allows you to run virtual machines (VMs) on a variety of host operating systems.

- Check version

> `virtualbox version`

- Install Vagrant

> `brew cask install virtualbox`

- Vagrant upgrade

> `brew cask upgrade virtualbox`

## 3. Create and Configure Vagrant

NOTE: FOR THIS MIXED CONFIG TO SKIP SOME OF THESE STEPS, DOWNLOAD THE REPO and `vagrant up` It will have shell scripts in the `/scripts` folder with the following installations consolidated into `.sh` files and all portfowarding and share file paths added to the Vagrantfile.

> git@github.com:jamesahnking/hlf-dev-env-01.git


- Create project directory

- Inside of the project directory type

> `vagrant init`

- To install a box at initilization

> `vagrant init bento/ubuntu-16.04`

- Add version tracking with `Git`

- The `vagrant init` command creates a new file called `Vagrantfile`.

> `vagrant init`

- The `Vagrantfile` Marks the root directory of your project. Many of the configuration 
options in Vagrant are relative to this root directory.

- The `Vagrantfile` describes the kind of machine and resources you need to run your project, as well as what software to install and how you want to access it.

- Open `Vagrantfile` to configure if needed

> `vim Vagrantfile`

Clone the following repo, replace Vagrant file and add diretories. 

> https://github.com/acloudfan/HLF-Vagrant-Dev-Setup

- To update box

> `vagrant update box`

- Start Vagrant

> `vagrant up`

- View config info

> `vagrant ssh-config`

- Login to server

> `vagrant ssh`

## 4. Install Hyperledger prereqs on VM

- Install Hyperledger prereqs on VM: - All prerquisites can be installed at once with:

> `curl -O https://hyperledger.github.io/composer/latest/prereqs-ubuntu.sh` 

- Change permissions - u+x makes the file executable

> `chmod u+x prereqs-ubuntu.sh`

- Execute File `.sh` file

>`./prereqs-ubuntu.sh`

## Installed Prereqs

> <https://hyperledger.github.io/composer/latest/installing/installing-prereqs.html#ubuntu> 

Docker Cheatseat:
> <https://github.com/wsargent/docker-cheat-sheet>

- Docker Engine: `Version 17.03` or higher

- Docker-Compose: `Version 1.8` or higher

- Node: `8.9` or higher (note version 9 and higher is not supported)

- npm: `v5.x`

- git: `2.9.x` or higher

- Python: `2.7.x`

## Installing Hyperledger Fabric and Composer on VM

> <https://hyperledger.github.io/composer/latest/installing/development-tools.html>

- `Hyperledger Composer` is an application development framework which simplifies and expedites the creation of Hyperledger fabric blockchain applications.

- `Hyperledger Fabric` is a blockchain framework implementation for developing applications or solutions with a modular architecture that allows components, such as consensus and membership services, to be plug-and-play. Hyperledger Fabric leverages container technology to host smart contracts called `chaincode` that comprise the application logic of the system

## 5. Install CLI tools on VM

- Essential CLI tools:

> `npm install -g composer-cli@0.20`

- Utility for running a REST Server:

> `npm install -g composer-rest-server@0.20`

- Utility for generating application assets:

> `npm install -g generator-hyperledger-composer@0.20`

- Yeoman tool generates application and utilize`

> `generator-hyperledger-composer` : `npm install -g yo`    

## 6. Install Playground on VM

- Playground browser app for testing BNs: 

> `npm install -g composer-playground@0.20`

> `npm uninstall -g composer-playground`

- Set up `VSCode` with `Hyperledger Composer` extention from the Marketplace

## 7. Verifying Installation on VM

Verify node JS

> `node -v`

Run the command to check the version of composer CLI

> `composer -v`

Execute the following command to see if the Composer tool is working

> `composer -h`

Check if the hyperledger-composer yo generator is installed

> `yo --generators`

## 8. Install Hyperledger Fabric on VM

- Create a directory `~/fabric-dev-servers` :  

> `mkdir ~/fabric-dev-servers && cd ~/fabric-dev-servers`

- Download `.tar.gz` file:

> `curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz`

- Extract:

> `tar -xvf fabric-dev-servers.tar.gz`

- Download Hyperledger Runtime.

> `./downloadFabric.sh`

- Start Hyperledger: if you run `./startFabric.sh` before `./downloadFabric.sh` it will auto install Fabric images

> `./startFabric.sh`

- Check Docker containers

> `docker ps`

- Test when containers status, repeating once a second

>`watch -n 0.1 'docker ps '`

---

## 9. Configuring Environment with `docker-machine` on `HOST`

`Docker Machine` is a tool that lets you install `Docker Engine` on virtual hosts(`VM`), and manage the `VM` with `docker-machine` commands.

Using Docker Machine with VM Documentation
> <https://docs.docker.com/machine/get-started/>

Docker Machine Reference
> <https://docs.docker.com/machine/reference/env/>

`Docker Machine` is a tool that lets you install `Docker Engine` on virtual hosts, and manage the hosts with `docker-machine` commands. You can use `Machine` to create `Docker` hosts on your local Mac or Windows box, on your `company network`, in your `data center`, or on `cloud providers` like `Azure, AWS, or Digital Ocean`.

Using `docker-machine` commands, you can `start`, `inspect`, `stop`, and `restart` a managed host,upgrade the Docker client and daemon, and configure a Docker client to talk to your host.

We point the `Machine CLI` at a running, managed host, and you can run docker commands directly on that host.

** On the `HOST machine`  **

Attach the current VM to the `docker-machine`
> `docker-machine create -d generic --generic-ip-address <ip> --generic-ssh-key <keypath> --generic-ssh-user <user> --generic-ssh-port 22 <vm name>`

Current Working Example:

> `docker-machine create -d generic --generic-ssh-user vagrant --generic-ssh-key /Users/jamesahnking/Dropbox/050_Kellan_Partners_LLC/000_Development/24_VagrantFabricNetworks/001_khlf_Network/.vagrant/machines/default/virtualbox/private_key --generic-ssh-port 2222 --generic-ip-address 127.0.0.1  default`

---

**On the HOST machine add the following to your `Vagrant` file to port forward for VM access.**

> `Configure port forwarding to support remote access to Docker Engine`
> `config.vm.network "forwarded_port", guest: 2376, host: 2376`

---

To kill a `docker-machine` if a mistake is made

> `docker-machine rm <machinename>`

You will be prompted to connect your `Docker Client` to the `Docker Engine` running the `VM`, 

Run: `

> `docker-machine env default`

This will display the newly configured environment variables and prompt to configure your shell:
Also, when visibility is lost on the VMs docker images and containers run `eval $(docker-machine env default)` to bring it back.

> `eval $(docker-machine env default)`

Validate by checking docker images on the VM from `HOST` machine run:

> `docker images`

VM `hyperledgerimages` that should be viewable from host `default`

|REPOSITORY       |            TAG       |          IMAGE ID      |      CREATED      |       SIZE|
|---------------- | -------------------- | ---------------------- | ------------------|-----------|
|hyperledger/fabric-orderer  | 1.2.1     |        b1a1dd788841    |   4 months ago  |     152MB   |
hyperledger/fabric-peer       | 1.2.1    |          ef0e7788ead0  |      4 months ago   |     159MB
hyperledger/fabric-ca         | 1.2.1    |         be8400395e15    |    4 months ago    |    251MB
hyperledger/fabric-couchdb  | 0.4.10     |          3092eca241fc   |     7 months ago    |    1.61GB



For BASH to reset Environment Variables run
> `unset ${!DOCKER_*}`

Alternate unset Evironment
> `eval $(docker-machine env -u)`

- Validate ability to view docker images in VM
> `docker-machine ls`

## Add Fabric Utility Shell Script

Create `./fabricUtil.sh'` and add to `~/.fabrick-def-servers` on the VM this file is not included in the Fabric installation.`./startFabric.sh` Kills and Removes running containers and deployed applications are REMOVED. This is why we use `./fabricUtil.sh` 

Link to shell script :

> <https://github.com/acloudfan/HLF-Windows-Fabric-Tool/blob/master/fabricUtil.sh>

## Practice! Start, Stop, Suspend, Restart

- Launch your dev environment

#### On Host

> `vagrant up`

>`vagrant ssh`

#### On VM

> `cd ~/fabric-dev-servers`

> `./startFabric.sh`

- Use the Docker command from `HOST` to check if all of the 4 containers for farbric environment are up 

> `docker ps`

To check the logs 
> `docker logs --tail 10 peer0.of1.peername.com`

- Now suspend the environment

> `./fabricUtil.sh stop`

- Run the docker command (ps) from host... you should not see the containers

> `docker ps`

- Run the docker command (docker ps -a) ... you should see the dangling/suspended containers. 

> `docker ps -a`

- Re-start the environment using `fabricUtil` using docker to check if the containers are up

> `./frabricUtil.sh start`

> `docker ps`

- Use `stopFabric`

> `./stopFabric.sh`

Then check the status of the containers. Do you see the suspended containers?

> `docker ps`

> `ps -a command`

## Create Peer Admin Card to manage network

> 'cd ~/fabric-dev-servers'
> 
> export FABRIC_VERSION=hlfv12

> ./startFabric.sh

> ./createPeerAdminCard.sh

## Tips and Tricks
comp
Dev Setup and Tips
<https://github.com/acloudfan/HLF-Vagrant-Dev-Setup>
