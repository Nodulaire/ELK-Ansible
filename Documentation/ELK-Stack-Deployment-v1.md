# ELK Stack deployment

## Aim of the document

Here we are going to see how to deploy the entire ELK Stack on each host.

## Summary

1 - [Playbooks Strucutre](#playbooks-strucutre)  
2 - [ELK playbooks Skeleton](#elk-playbooks-skeleton)  
3 - [ELK deployment Playbook](#elk-deployment-playbook)

## Playbooks Strucutre

(The structures showed below are obtained by the *tree* unix command made by Steve Baker).  

Each playbook follows this structure :

```
XXX
├── defaults
│    └── XXX_options.yml
└── tasks
     └── install_XXX.yml

```

The file <i> defaults/XXX_options.yml </i> contains all variables (default values, path, version, etc...) used in <i> tasks/install_XXX.yml </i>.

## ELK playbooks Skeleton

Here is our entire ELK structure for the installation :

```
playbooks/
├── elk
│   ├── defaults
│   │   └── elk_options.yml
│   ├── elasticsearch
│   │   ├── defaults
│   │   │   └── elasticsearch_options.yml
│   │   └── tasks
│   │       └── install_elasticsearch.yml
│   ├── kibana
│   │   ├── defaults
│   │   │   └── kibana_options.yml
│   │   └── tasks
│   │       └── install_kibana.yml
│   ├── logstash
│   │   ├── defaults
│   │   │   └── logstash_options.yml
│   │   ├── src
│   │   │   ├── 10-syslog.conf
│   │   │   ├── ca.pem
│   │   │   ├── elk-cert.pem
│   │   │   └── elk-key.pem
│   │   └── tasks
│   │       └── install_logstash.yml
│   ├── nginx
│   │   ├── defaults
│   │   │   └── nginx_options.yml
│   │   └── tasks
│   │       └── install_nginx.yml
│   └── tasks
│       └── install_elk.yml
└── java
    └── install_java.yml
  ```

### ELK deployment Playbook

The file <i> elk/tasks/install_elk.yml </i> is our general deployment playbook. It calls all necessary playbooks of the stack.

```yml
---
- hosts: ELK
  remote_user: root
  tasks:
    - include_vars: '/home/administrateur/playbooks/elk/defaults/elk_options.yml'
    - include: '{{java_path}}/install_java.yml'
    - include: '{{elk_path}}/elasticsearch/tasks/install_elasticsearch.yml'
    - include: '{{elk_path}}/kibana/tasks/install_kibana.yml'
    - include: '{{elk_path}}/nginx/tasks/install_nginx.yml'
    - include: '{{elk_path}}/logstash/tasks/install_logstash.yml'

    - name: Install packages
      apt:
        name={{item.paquet}}
        update_cache=yes
        state=present
      with_items:
        - { paquet: "rsyslog-gnutls" }
        - { paquet: "gnutls-bin" }
        - { paquet: "aptitude" }
      tags: [ELK]     

    - name: Upgrade packages
      apt: upgrade=yes
      tags: [ELK]    
```

Thanks !  
**Boboo**
