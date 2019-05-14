# sparta-vagrant-nodejs

This repository holds a provisioned __dev environment__ for a __NodeJS application__. The following tools have been utilised to create the dev environment. This ReadMe will be useful to anyone hoping to create a dev environment for nodeJS development. You can either git clone the provisioned environment or recreate the whole environment using the steps below.

## Tools used
- __Linux Ubuntu Xenial64__ – Operating system
- __Node JS version 6__ – JS backend library
- __Nginx__ – Webserver
- __Vagrant__ - Managers VM environments
- __Oracle Virtual box__ - Hypervisor
- __PM2__ – Package manager for nodeJS applications
- __Ruby__ – Scripting language

## Two ways of using this repo or ReadMe
1)	Recreate by yourself by following the all the steps below
2)	Git clone this repo and ensure all steps are present.

#### Step 1
Install the required tools, vagrant and virtual box.

Virtual box is the type 2 hypervisor that runs on top your Operating system and runs Linux as a Virtual Machine. Vagrant is a provisioning tool that eases the spawning of VMs. They both work together to ease the provisioning of your dev environment.

#### Step 2
On your terminal, make the required folders

mkdir devops
cd devops
mkdir dev-environment
Cd dev-environment

#### Step 3
On your mac terminal start vagrant. Test vagrant is installed with the command `vagrant`, this should result in vagrant commands help list.

#### Step 4
Run

`Vagrant init ubuntu/xenial64`

This will install the linux ubuntu operating system as a virtual machine VM on the hypervisor.

This will create a vagrant file in your dev-environment folder, you will also see a ubuntu console log file.


#### Step 5
open using your code editor such as Atom with the command

`atom .`

#### Step 6

On the vagrant file in your atom editor add the following ruby code.

`Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network("private_network", ip:"192.168.10.100")
end`

vagrant class uses a loop and uses the configure method, loops through config available list of files available.

Uses a static IP to access your application through your chosen web browser.

#### Step 7
vagrant plugin install `vagrant-hostsupdater`   

use the above command to install the hosts updater plugin

#### Step 8
add the following ruby code to vagrant file
`config.hostsupdater.aliases = ['development.local']``


#### Step 9
run on terminal

`Vagrant up`

This creates the environment

#### Step 10  
run on terminal

`Vagrant ssh`

This uses secure shell (SSH) protocol to enable you to use the terminal inside the ubuntu VM which is running on top of the virtual box hypervisor.

`Sudo apt-get update`

`Sudo apt-get install nginx`

`Sudo systemctl start nginx`

Type development.local/  into browser

You should see the nginx start page in your browser

The first 10 steps allow you to create an environment manually, the next steps will show you how to provision this environment using a bash script.

#### Step 11

`Git clone` the following node js app

https://github.com/spartaglobal/node-sample-app

or git clone this repo and check the following steps are correct, they should already be included if you clone this repo.

#### Step 12

Git clone environment folder, this contains the rspec files to test the dev environment requirements.

#### Step 13

Create a provisioning.sh file inside the environment folder

#### Step 14

Link provisioning file with vagrant by adding the following line of code into Vagrant file.

  `config.vm.provision("shell", path:"environment/provision.sh")``

#### Step 15

add following command to

`sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install nginx -y
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install -g pm2
cd /app
pm2 start app.js --name="My Awesome App"`


#### Step 16

run

`vagrant destroy`

run

`vagrant up`

this will create a new environment and include your provinsing.sh file.

#### Step 17

View the app on http://development.local:3000/
