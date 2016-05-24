# ANSIBLE installation


Ansible is a simple IT automation engine that automates cloud provisioning, configuration management, application deployment, intra-service orchestration, and many other IT needs.  
*ansible.com*  

<center>![ansible logo](Documentation/Images/Ansible/ansible_logo.png)</center>
## Aim of the document

  Here we are going to deploy and test a basic ANSIBLE installation. It mean installation from the depository, configuration and test on a remote host.

## Principe

Written in python it permit the configuration of remote hosts like you used to do with bash scripts, but way better.
Ansible can handle all the errors and you can create pattern depending of the error returned by the remote host. Better, the same book can be played multiple time without harming the system or the previously installed playbook.

### Playbooks

It's the name given to the prog names written in ansible. They centralize all the roles, actions and variables used for the services installation on remote hosts. You want them to be the less specific possible to be compliant with as many system as possible.
The language used in playbook is .yaml, wich is just an optimised XML.
