
---
# {{appliance-name}}
## Installation Manual


*Document Control*    

|  Date | Version  | Author  | Change/Addition  |
|---|---|---|---|
| 22/08/2016  |0.1| Renaud PULIDO  |  Creation |



## Table of Contents

1 - [Introduction](1 - Introduction)   
  1.1 [Aim of this document](1.1 Aim of this document)   
  1.2 [Audience](1.2 Audience)  
  1.3 [Revision warning](1.3 Revision warning)   
2 - [Product deployment](2 - Product deployment)  
2.1 [Targeted OS](2.1 Targeted OS)  
2.2 [Hardware requirement](2.2 Hardware requirement)  
2.3 [Deployment technologie](2.3 Deployment technologie)  
2.4 [Pre-configuration](2.4 Pre-configuration)  
3 - [Installation](3. Installation)  

---

## 1 - Introduction
### 1.1 Aim of this document  
This document describes the installation process for {{appliance-name}}.  
It holds all necessary information for the installation on a single or multiple machine.

### 1.2 Audience  

This document is primarily intended to be used by Operations staff for automatised installation and custom configuration.
The product ain't aimed to be installed manually on the servers.

### 1.3 Revision warning  
As the {{appliance-name}} is still in developement, the instructions may change from the reality.  
Contact rpulido{at}sii{dot}fr to be keeping in touch.

---

## 2 - Product deployment

### 2.1 Targeted OS
 As mentionned in the TSD, the only supported OS is *Ubuntu 16.04.1 LTS (Xenial Xerus) x64*.
 The product can be deployed in other OS but no documentation will be made.

### 2.2 Hardware requirement

Depending on the need there is a quick (by architecture deployment see TSD):  

|  Capacity/Products | Monolithique infrastructure  | Stacked clusters  |
|---|---|---|
| Servers |  1| 6 (at least)  |
| Total min. CPU capacity| 4c/4t| 12c/24t |
| Total min. RAM capacity| 4Go*| 24Go* |
| Disk capacity/monthly | up to 155Go | up to 28To |

### 2.3 Deployment technologie

Ansible, as been choosed for its incredible capacity and adaptivity.
You can install it with ```sudo apt inst ansible```.   
See also : [Ansible-install-v1](https://github.com/Nodulaire/ELK-Ansible/blob/master/Documentation/Ansible-Install-v1.md)  
{{appliance-name}} is only deployable with Ansible.

### 2.4 Pre-configuration

All the user-defined variable are on the file : [Playbooks/site.yml](https://github.com/Nodulaire/ELK-Ansible/blob/master/Playbooks/site.yml)  
Adapt those variables with the client needs.

---

## 3. Installation

Once everything set up, launch the playbook (see the [related topic](https://github.com/Nodulaire/ELK-Ansible/blob/master/Documentation/Ansible-Install-v1.md#launching-the-playbook))  
Let the playbook until its finish. It's all done.

Here end the installation manual and start the Configuration & Operation instruction guide.
