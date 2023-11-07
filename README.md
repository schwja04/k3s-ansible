## What is the purpose of this repository?
The primary goal of this solution is to provide an "easy button" deployment of a k3s cluster. It is also providing me a playground to improve my understanding of ansible playbooks.

This project was based on a blog and accompanying repository created by Techno Tim. The goal was to reduce the generic nature of the implementation provide in his blog to only the core pieces needed for my project.

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
1. Ensure that you have ansible installed.
1. Run `ansible-galaxy install -r collections/requirements.yml`
1. The solution should be ready at this point for you to run `ansible-playbook install.yml`

## I think I made a mistake, what can I do?
If you have a need to restart as if no install job ran, you can run the uninstall playbook. Your machines should be as if the install job never ran.