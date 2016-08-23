
---
# {{appliance-name}}
## Technical Service Description

*Document Control*    

|  Date | Version  | Author  | Change/Addition  |
|---|---|---|---|
| 22/08/2016  |0.1| Renaud PULIDO  |  Creation |


## Table of Contents

1 - [Introduction](#Introduction)  
  1.1 [Document purpose](#Document purpose)    
  1.2 [Audience](#Audience)   
2 - [ELK Overview](#ELK Overview)   
  2.1 [Open source consideration](#Open source consideration)   
  2.2 [About {{appliance-name}}](#About {{appliance-name}})   
  2.3 [Selection crietria](#Selection crietria)   
  2.4 [Global limits & constraints](#Global limits & constraints)
3 - [Architecture](#Architecture)  
  3.1 [Covered functions](#Covered functions)    
  3.2 [Monolithique infrastructure](#Monolithique infrastructure)  
    3.2.1 - [Design](#Design)  
    3.2.2 - [Pro](#Pro)  
    3.2.3 - [Con](#Con)  
  3.3 - [Stacked clusters](#Stacked clusters)  
    3.3.1 - [Design](#Design)  
    3.3.2 - [Pro](#Pro)  
    3.3.3 - [Con](#Con)    
  3.4 - [Hardware / software prerequisites](#Hardware / software prerequisites)  
    3.4.1 - [Hardware requirement comparaison](#Hardware requirement comparaison)    
    3.4.2 - [Backup](#Backup)
  3.5 - [Network and flows](#Network and flows)
  3.6 - [Authentication services](#Authentication services)
  3.7 - [Security policy & strategy](#Security policy & strategy)

---

## Introduction
### Document purpose   
This document provide a low level technical information to be taken into account
when implementing ELK.    

It does **NOT** include best practices, which should be found in the *Administration Guide*.  

This document will also justify the technological decision who where made during this project.   

### Audience

The TSD is a reference document for all enineering team members who have to work on this specific product.

Basic knowledge on networking and virtualization technologies are required.

This document may also be used by Sales Support staff as a base for their High/Low Level Design documents specific to every bid.

---
## ELK Overview  
### Open source consideration  

Only open-sources solutions are used and implemented on this project. Set apart the financial aspect, there-is many advantages for the open-sources solution:  
- **Security**: Open to public view the code is easly audited and security flaw are rapidly found and patched.   
- **Customizability**: Along similar lines, we can take a piece of open source code and tweak it to suit our needs., without reinventing the wheel.
- **Interoperability**: Unlimitted by proprietary data formats, open source software is the way to interact whit multiple hardware and technologies.

###  About {{appliance-name}}   

The following sections describe the products and component software available in {{appliance-name}}: Logstash (data processor / parser), Elasticsearch (the database), Kibana (Graphic Interface), Suricata (Networking IDS).

{{appliance-name}} is a solution who aim to provide a SIM (Security Information Management) monitoring plateform, universal and easy to use/deploy.  

#### About Logstash
![logstash](../Images/logo/logstash_logo.png)

Logstash is a data pipeline that helps you process logs and other event data from a variety of systems. With 200 plugins and counting, Logstash can connect to a variety of sources and stream data at scale to a central analytics system.   

Business-critical data is often scattered among different systems, each in its own format. Logstash allows you to parse this data and converge on a common format before inserting it into your analytics datastore of choice.  

Most logs written by infrastructure and applications have custom formats. Logstash provides a fast and convenient way to custom logic for parsing these logs at scale.  


#### About Elasticsearch
![elasticsearch](../Images/logo/logo-elastic.png)   

Elasticsearch is a search engine based on Lucene. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. It's:
- Distributed, scalable, and highly available
- Real-time search and analytics capabilities
- Sophisticated RESTful API


#### About Kibana   

![kibana](../Images/logo/logo-elastic-kibana-lt.png)

Architected to work with Elasticsearch, Kibana gives shape to any kind of data — structured and unstructured — indexed into Elasticsearch. It also benefits from Elasticsearch's powerful search and analytics capabilities.  

- Flexible analytics and visualization platform
- Real-time summary and charting of streaming data
- Intuitive interface for a variety of users
- Instant sharing and embedding of dashboards

#### About Suricata

![suricata](../Images/logo/suricata.gif)

Suricata is a high performance Network IDS, IPS and Network Security Monitoring engine. Open Source and owned by a community run non-profit foundation, the Open Information Security Foundation (OISF). Suricata is developed by the OISF and its supporting vendors.
- Highly Scalable
- Protocol Identification
- File Identification, MD5 Checksums, and File Extraction

### Selection criteria   

This is the “readme-first” section that presales support would use to rapidly identify potential architecture or options {{appliance-name}} offers.

|  Capacity/Products | {{appliance-name}}  | Splunk  | OSSIM  |
|---|---|---|---|
| Open-Source   |  ✔| ✘  |  ✔ |
| Free   |  ✔ | ✘*  |  ✔ |
| Clusterable   |  ✔ | ✘  |  ✘ |
| Independant database   |  ✔| ✘  |  ✘ |
| Big-data Ready   |  ✔| ✔  |  ✘ |
| Agent-less |  ✔ | ✘  |  ✘ |
| End to end encryption|  ✔| ✔  |  ✘ |

(\*Free for less than 500mo/day)

### Global limits & constraints

The hardware is the only limit to {{appliance-name}} (up to 1To/logs day). Sizing is very important and must fit your needs (present and future).

The only supported OS is *Ubuntu 16.04.1 LTS (Xenial Xerus)*. The product can be deployed in other OS but no documentation will be made.

---

## Architecture

The next sections cover individual architectures or options for {{appliance-name}}

### Functions covered (logical design)
### Monolithique infrastructure
#### Design
#### Pro
Easiest and speedest setup to install, it can be deployed in 10minutes (with the correct setup) and configured in a day (dependings of the technology on site).   
Perfect for small business.
#### Con
It's slower and can't process more than 5Go/logs per day.
### Stacked clusters
#### Design
#### Pro
Hardest installation, can take up to few hours, and weeks to configure (depending of the client infrastructure). It can handle up to 900Go/logs per day with the correct amount of hardware.
Perfect for middle and big business.
#### Con
Slow to deploy and greedy in hardware ressources.
### Hardware / software prerequisites
#### Hardware requirement comparaison  
|  Capacity/Products | Monolithique infrastructure  | Stacked clusters  |
|---|---|---|
| Servers |  1| 6 (at least)  |
| Total min. CPU capacity| 4c/4t| 12c/24t |
| Total min. RAM capacity| 4Go*| 24Go* |
| Disk capacity/monthly | up to 155Go | up to 28To |


(\* Elasticsearch using Java,  you can only feed 50% of the hardware ressources to {{appliance-name}}, so in fact it's 12Go for the SIM and what's left stay for the OS.)

#### Software requirement
As specified on *2.4*, the only supported OS is *Ubuntu 16.04.1 LTS (Xenial Xerus)* with python 2.7 installed and a sudo ssh access.  

#### Backup

Refer to the corporate backup policie.

### Network and flows

| Num|  Source| Destination | Protocol  | Port | Comments
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | All the monitored systems/applications | Logstash servers | TCP/TLS | User defined (>1024) | Main entry point of the SIM |
| 2| Suricata VM | Logstash servers | TCP/TLS | User defined (>1024) | IPS logs entry |
| 3 | Logstash servers | Elasticsearch cluster | TCP/TLS | User defined (>1024) | Database entry |
| 4 | Kibana | Elasticsearch cluster | TCP/TLS | User defined (>1024) | Monitoring entry |
| 4 | Admin network | Kibana | HTTPS | User defined (>1024) or 443  |Kibana Web interface |

### Authentication services

SSH identity are used for the installation process.  
Concerning the monitoring web interface, no authentification service is installed.  

### Security policy & strategy
At this point (R&D) no security strategies are planned.


---

That's all folks !  
Thanks for reading,  
**Nodulaire**
