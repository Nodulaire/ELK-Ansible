# Elasticsearch

## Summary
1 - [Definition](#Definition)  
2 - [Installation](#Installation)  

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
