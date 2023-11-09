## What is the purpose of this repository?
The primary goal of this solution is to provide an "easy button" deployment of a k3s cluster. It is also providing me a playground to improve my understanding of ansible playbooks.

This project was based on a blog and accompanying repository created by Techno Tim. The goal was to reduce the generic nature of the implementation provide in his blog to only the core pieces needed for my project.

This solution proved successful when I deploy via a fresh install of Ubuntu 22 for my ansible controller, control nodes and agent nodes. **Warning**. The most difficult part of this process for me was getting the ansible controller configured properly.

## What do I need to change?
### Variables
Under group_vars, create a copy of `all-template.yml` named `all.yml`.
```bash
cp all-template.yml all.yml
```
Locate the `<REPLACE>` strings throughout the file with relevant values.

### Inventory
Under inventory, create a copy of the `template-hosts.ini` named `hosts.ini`.
```bash
cp template-hosts.ini hosts.ini
```
You will need to replace the ip addresses with the url or ip address of the machines that you are planning to host your cluster on. The current configuration is meant to deploy the control planes in a highly available fashion.

## What do I need to do before I run this?
1. Ensure that you have ansible >2.11 installed. I personally had a lot of issues with compatibility some commands had been moved from one module to another. To get the newest version of ansible on my ansible controller, I had to do the following:
    1. Uninstall ansible if it was already installed on the machine. `sudo apt remove ansible -y`
    1. Purge the purge apt. `sudo apt --purge autoremove`
    1. sudo apt update -y && sudo apt upgrade -y
    1. sudo apt install software-properties-common -y
    1. sudo apt-add-repository ppa:ansible/ansible
    1. sudo apt install ansible
1. Run `ansible-galaxy install -r collections/requirements.yml`
1. Run `pip3 install -r requirements.in`
    - This left warnings in the console, but were red herrings.
1. The system should be ready at this point for you to run `ansible-playbook install.yml`

## I think I made a mistake, what can I do?
If you have a need to restart as if no install job ran, you can run the uninstall playbook. Your machines should be as if the install job never ran.