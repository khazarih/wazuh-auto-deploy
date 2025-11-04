# Wazuh Deployment Automation 
This repo is intended for automating Wazuh deployment using Vagrant and Virtualbox for testing and development.
Currently, during the setup, only one instance for each component is installed for Wazuh (indexer, server and dashboard).
Follow the steps below to proceed with deployment.

## Requirements
Tests has been done on Fedora 42. However, it should be similar in almost every other environment.
- Vagrant
- Virtualbox
- Enough RAM and CPU cores

If you are out of RAM or CPU cores, just check the minimum requirements for each componenet of Wazuh, and update Vagrantfile accordingly for your environment.

For Virtualbox network configuration, if you haven't changed anything in the Virtualbox network settings, you should be good to go without any changes to the Vagrantfile. 

However, if you have changed your default subnet before(default: 192.168.56.0/24), you will need to update IP address for each component in the Vagrantfile to match with your custom network settings.

## Install Vagrant
Follow the instructions in the link to install Vagrant on your host OS: https://developer.hashicorp.com/vagrant/install

## Install Virtualbox
Follow the instructions in the link to install Virtualbox on your host OS: https://www.virtualbox.org/wiki/Downloads

## Deploy Virtual Machines
Clone the repository

```bash
git clone https://github.com/khazarih/wazuh-auto-deploy.git
```

Run vagrant up

```bash
vagrant up
```

Once deployment has finished, you should see username and password in the terminal output which will be used for authentication in the Wazuh dashboard.

Go to Wazuh dashboard in your browser and enter creds: 
https://192.168.56.30


