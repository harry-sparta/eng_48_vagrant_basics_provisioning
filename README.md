# [09:00] Notes from Daniel

## How to use this environment
- Download vagrant from vagrantup.com
- Download virtualbox from virualbox.org
- Make a new directory and move app to this directory
- From your terminal run vagrant init to create a vagrant file in this new directory
- In this vagrant file you can then configure the settings for your virtual environment. In general:
  - config.vm.box - operating system
  - config.vm.network - How your host sees your box
  - config.hostsupdater.aliases - How to give an alias for the IP
  - config.vm.synced_folder - How you access files from your local machine/computer
  on the VM (syncing your local folder with your vagrant box folder)
  - config.vm.provision - what we want to setup (automating the setup process)


- Use the xenial64 machine by inputting: config.vm.box = "ubuntu/xenial64"
into the vagrant folder
- sync your folders by inputting: config.vm.synced_folder "app", "/app"
into the vagrant folder
- Spin up the VM (create the VM) by running vagrant up in the terminal
- SSH into the box (make a connection to the VM) by running vagrant ssh
- create a provision.sh file in the environment folder so that you can provision the machine
- input this into the provision.sh file:
#!/bin/bash
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install nginx -y
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs -y
sudo npm install pm2 -g
cd /app
npm install
npm start
- In the vagrant file input:
config.vm.provision "shell", path: "environment/provision.sh"
