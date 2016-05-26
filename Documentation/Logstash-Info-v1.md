# Logstash

## Summary
1   - [Definition](#definition)   
2   - [Installation](#installation)  
2.1 - [Variables file](#variables-file)  
2.2 - [Sources files](#sources-files)  
2.3 - [Install file](#install-file)
## Definition

"Logstash is an open source tool for collecting, parsing, and storing logs for future use." Wikipedia

Logtsash collect and process all the log he received. It's support a lot of format but here we are only using syslogformat ( RFC 5424 ) and JSON to get all our logs togethers and understandable for elasticsearch.

## Installation

The Installation of logstash is part of our ELK deployement playbook. Here we're gonna explain the files contain.
### Variables file

You can find this file [here](../Playbooks/elk/logstash/defaults/logstash_options.yml).

```yml
logstash_version: "2.3"
logstash_src_conf_path: "/home/administrateur/playbooks/elk/logstash/src/"
logstash_dst_conf_path: "/etc/logstash/conf.d/"
logstash_dst_certs_path: "/opt/rsyslog"
logstash_server_private_ip: "192.168.122.26"
logstash_rsyslog_path: "/etc/rsyslog.conf"
logstash_ssl_cfg: "/etc/ssl/openssl.cnf"
```

As the other playbook we their is the version, the address, and the path of files to configure.

## Sources files

Contrary to other playbooks, logstash integrate the *src* directory. It contains files which we directly transfer to the hosts.

TODO

## Install file

You can find this file [here](../Playbooks/elk/logstash/tasks/install_logstash.yml). I will describe the main part of the installation.

```yml
- include_vars: '/home/administrateur/playbooks/elk/logstash/defaults/llogstash_options.yml'
```

This line include each variables we need for the install. To use a variable, use this syntax *{{variable_name}}*.  

```yml
- name: Install Elasticsearch GPG Key
  apt_key: url=http://packages.elasticsearch.org/GPG-KEY-elasticsearch state=present
  tags: [logstash]
```
Here we add the *apt-key* for Elasticsearch repository. Then we add the repository which contains logstash with the Ansible function *apt_repository*.
```yml
- name: Add logstash repository
  apt_repository: repo='deb http://packages.elastic.co/logstash/{{logstash_version}}/debian stable main' state=present
  tags: [logstash]
  ```
The option *state=present* check if the repository is already installed.

Then we install logstash package with the function *apt* :
```yml
- name: Install Logstash
  apt: name=logstash update_cache=yes state=present
  tags: [logstash]
```
Then we copie the ELK server keys (locate in [playbooks/elk/logstash/src](#../Playbooks/elk/logstash/src)) on the host with a loop and th function copy :
```yml
- name: Add ELK Certificates
  copy:
    src={{item.copies}}
    dest={{logstash_dst_certs_path}}
  with_items:
    - { copies: "{{logstash_src_conf_path}}/ca.pem" }
    - { copies: "{{logstash_src_conf_path}}/elk-cert.pem" }
    - { copies: "{{logstash_src_conf_path}}/elk-key.pem" }
  tags: [logstash]
  ```
These certificates will be used in oder to secure the communication between the server and the hosts.  
We also add a logstash conf file from logstash [src](#../Playbooks/elk/logstash/src) directory.
```yml
- name: Add Logstash Conf
  copy:
    src={{item.copies}}
    dest={{logstash_dst_conf_path}}
  with_items:
    - { copies: "{{logstash_src_conf_path}}/10-syslog.conf" }
  tags: [logstash]
```
This file contain the "parser" for the logs. We use a loop even if there is only one file because it will be easier to add a file.

Then we add the log *rsyslog* to logstash :
```yml
- name: Add rsyslog to logstash
  lineinfile:
    dest='{{logstash_rsyslog_path}}'
    line='{{logstash_rsyslog_add}}'
  tags: [logstash]
```

After we create directories for the certificate we will generate :
```yml
 - name: Add certificate directory
   command: mkdir -p /etc/pki/tls/private /etc/pki/tls/certs
   tags: [logstash]
```
Here the certificate generation :
```yml
 - name: Add Logstash Certificates
   command: openssl req  -x509 -days 3650 -batch -nodes -newkey rsa:2048 -keyout /etc/pki/tls/private/logstash-forwarder.key -out /etc/pki/tls/certs/logstash-forwarder.crt
   tags: [logstash]
```

Finally we launch the service on boot then start it with the function *service* :
```yml
- name: Start Logstash on Boot
  service: name=logstash enabled=yes
  tags: [logstash]

- name: Starting Logstash
  service: name=logstash state=started
  tags: [logstash]
```  

Thanks !  
Boboo
