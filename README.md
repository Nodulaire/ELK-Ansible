# ELK-Ansible

## AIM 

Monitoring should be for everyone. Not only those with money or skills. Here we try to create a monitoring plateform, universal and easy to use. 

Here you are going to find :
 - ANSIBLE scripts ( automatisation of the installation ).
 - Logstash configuration files.
 - Elasticsearch configuration files.
 - Kibana dashboards ( exemples purpose ).
 - RSyslog configurations.
 - Plugins exemples for the log forwarding.


## Architecture 

### Principe
```
      ELK Stack Master                                           Client(s)
______________________________                        ______________________________   
|                            |                        |                            |  
|          KIBANA            |                        |          Web Logs          |  ___
|____________________________|                        |____________________________|    |
|                            |                        |                            |    |
|        ElasticSearch       |                        |        Systems Logs        |  __|
|____________________________|                        |____________________________|    |
|                            |                        |                            |    |
|         Logstash           |                        |        Kernel Logs         |  __|
|____________________________|                        |____________________________|    |
|                            |                        |                            |    |
|       Syslog Master        |  <--Client(s) Logs--   |        Local Syslog        |  <-/
|____________________________|         (TLS)          |____________________________|  
```
 In our solution all the clients send their logs (via TLS) directly to he stack syslog or to a legacy syslog server. 

### Maquette installation 

There is the infrastructure we use to test the product : 

![infra-maquette](https://github.com/Nodulaire/ELK-Ansible/blob/master/Documentation/Images/Maquette/infra-maquette.png)

## Pro/Con

### Pro 

- Agent less client configuration
- All log in the syslog standardised format
- No tierce software in the production servers
- Lightweight
- Compatible all Unix/Linux systems
- Integrity granted (TLS)

### Con
- Limited to  the supported rsyslog format 
- Specific logs input may need custom groks

### Hardware requirement
For this first version we are configuring the whole stack into a single (virtual) server. We will script multiple instance/cluster in a second time.


- ELK Stack server
      - OS  : Ubuntu Xenial 16.04 LTS
      - RAM : 4Go
      - CPU : 2
      - Oth : SSH Root acess and [python 2.7](http://docs.ansible.com/ansible/faq.html#how-do-i-handle-python-pathing-not-having-a-python-2-x-in-usr-bin-python-on-a-remote-machine) (not installed by default) and an internet connection.  

- Ansible server
      - RAM : 128Mo or more
      - OS  : Whatever who support SSH
      - Oth : Python 2.7





### TODO :
- Provide a docker contener (far far away in the future)
