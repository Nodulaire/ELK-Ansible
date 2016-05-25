# Elasticsearch

## Summary
1 - [Definition](#Definition)  
2 - [Installation](#Installation)  
2.1 - [Variables file](#variables-file)  
2.2 - [Install file](#install-file)

## Definition

Elasticsearch is a search server based on Lucene. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. Elasticsearch is developed in Java and is released as open source under the terms of the Apache License. *Wikipedia*

## Installation

The Installation of elasticsearch is part of our ELK deployement playbooks. Here we're gonna explain the files contain.

### Variables file

You can find this file [here](../playbooks/elk/elasticsearch/defaults/elasticsearch_options.yml).
```
# Default variables. Change as needed.

# Corresponding to file /etc/elasticsearch/elasticsearch.yml
es_cfg_file: '/etc/elasticsearch/elasticsearch.yml'
es_version: "2.3.1"
es_uid: 5500
es_gid: 5500
es_cluster_name: "ansible-es"
es_node_name: "ansible-es-1"
es_number_shards: 1
es_number_replicas: 0
es_path_conf: "/etc/elasticsearch"
es_path_data: "/var/lib/elasticsearch"
es_path_work: "/tmp/elasticsearch"
es_path_logs: "/var/log/elasticsearch"
es_path_plugins: "/usr/share/elasticsearch/plugins"
es_network_host: "0.0.0.0"
es_http_port: '9200'
```

Now I will describe the most significative options :  
* *es_cfg_file* : This is the path to the file we need to modify.  
* *es_version* : The version of elasticsearch you want to install (the lastest when I written this document)
* *es_cluster_name* : The name of the hosts cluster
* *es_node_name* : The name of the node (Host)
* *es_path_xxx* : File location
* *es_network_host* :
* *es_http_port* : Elasticsearch port

Obviously each option can be adapted to you architecture.

### Install file

You can find this file [here](../playbooks/elk/elasticsearch/tasks/install_elasticsearch.yml). I will describe the main part of the installation.

```
- include_vars: '/home/administrateur/playbooks/elk/elasticsearch/defaults/elasticsearch_options.yml'
```

This line include each variables we need for the install. To use a variable, use this syntax *{{variable_name}}*.  

This is an interesting Yaml syntax. Moreover it's a good example to explain and understand Yaml syntax.  

```
- name: Config Elasticsearch
  lineinfile:
    dest='{{es_cfg_file}}'
    line="{{ item.line }}"
    insertafter="{{ item.regexp }}"
    state=present
  ```


*lineinfile* is an Ansible function that search a string in a file then replace it or insert it by another one.  
Description :
  * *dest* : The file to parse
  * *line* : The line we want to insert after
  * *insertafter* : The string we are looking for. The keyword *insertafter* means that we want to insert the content of the variable *line* after the match and NOT INSTEAD of.
  * *state* : We insert only if *insertafter* match.

```
 with_items:
   - { regexp: '^# cluster.name', line: 'cluster.name: {{es_cluster_name}}' }
   - { regexp: '^# node.name',    line: 'node.name: {{es_cluster_name}}' }
   - { regexp: '^# http.port:',   line: 'http.port: {{es_http_port}}' }
   - { regexp: '^# path.logs',    line: 'path.logs: {{es_path_logs}}' }
 tags: [elasticsearch]
```
The second part of this function is a "loop". If we read closely, the arguments *line* and *insertafter* are defined by a variable. We instantiate *line* and *inserafter* variables by the couple *item.line* and *item.regexp* defined after the tag *with_items*.

Finally we launch the service on boot then start it with the Ansible function *service*:
```
- name: Start Elasticsearch on Boot
  service: name=elasticsearch enabled=yes
  tags: [elasticsearch]

- name: Starting Elasticsearch
  service: name=elasticsearch state=started
  tags: [elasticsearch]
  ```

  Thanks !
