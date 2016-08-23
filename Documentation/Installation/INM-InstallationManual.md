# {{appliance-name}}
## Installation Manual


*Document Control*    

|  Date | Version  | Author  | Change/Addition  |
|---|---|---|---|
| 22/08/2016  |0.1| Nodulaire  |  Creation |



## Table of Contents

1 - [Introduction](#Introduction)   
  1.1 [Aim of this document](#Aim of the document)   
  1.2 [Audience](#Audience)  
  1.3 [Revision warning](#Revision warning)   
2 - [Product deployment](#Product deployment)  
  2.1 [Targeted OS](#Targeted OS)  
  2.2 [Hardware requirement](#Hardware requirement)  
  2.3 [Deployment technologie](#Deployment technologie)  
  2.4 [Pre-configuration](#Pre-configuration)  
3 - [Installation](#Installation)  

---

## Introduction
### Aim of this document  
This document describes the installation process for {{appliance-name}}.  
It holds all necessary information for the installation on a single or multiple machine.

### Audience  

This document is primarily intended to be used by Operations staff for automatised installation and custom configuration.
The product ain't aimed to be installed manually on the servers.

### Revision warning  
As the {{appliance-name}} is still in developement, the instructions may change from the reality.  
Contact rpulido{at}sii{dot}fr to be keeping in touch.

---

## Product deployment

### Targeted OS
 As mentionned in the TSD, the only supported OS is *Ubuntu 16.04.1 LTS (Xenial Xerus) x64*.
 The product can be deployed in other OS but no documentation will be made.

### Hardware requirement

Depending on the need there is a quick (by architecture deployment see TSD):  

|  Capacity/Products | Monolithique infrastructure  | Stacked clusters  |
|---|---|---|
| Servers |  1| 6 (at least)  |
| Total min. CPU capacity| 4c/4t| 12c/24t |
| Total min. RAM capacity| 4Go*| 24Go* |
| Disk capacity/monthly | up to 155Go | up to 28To |

### Deployment technologie

Ansible, as been choosed for its incredible capacity and adaptivity.
You can install it with ```sudo apt install ansible```.   
See also : [Ansible-install.md](Ansible-Install.md)  
{{appliance-name}} is only deployable with Ansible.

### Pre-configuration

All the user-defined variable are on the file : [Playbooks/site.yml](https://github.com/Nodulaire/ELK-Ansible/blob/master/Playbooks/site.yml)  
Adapt those variables with the client needs.

---

## Installation

Once everything set up, launch the playbook (see the [related topic](https://github.com/Nodulaire/ELK-Ansible/blob/master/Documentation/Ansible-Install-v1.md#launching-the-playbook))  
Let the playbook until its finish. It's all done.

Here end the installation manual and start the [Configuration & Operation instruction guide](../Configuration/COI-ConfigurationAndOperationInstruction.md).



That's all folks !  
Thanks for reading,  
**Nodulaire**
