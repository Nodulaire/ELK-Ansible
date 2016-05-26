# Logstash

## Summary
[Definition](#Definition)   

## Definition

"Logstash is an open source tool for collecting, parsing, and storing logs for future use." Wikipedia

Logtsash collect and process all the log he received. It's support a lot of format but here we are only using syslogformat ( RFC 5424 ) and JSON to get all our logs togethers and understandable for elasticsearch.

## Installation

he Installation of logstash is part of our ELK deployement playbooks. Here we're gonna explain the files contain.
### Variables file

You can find this file [here](../playbooks/elk/logstash/defaults/logstash_options.yml).

```
logstash_version: "2.3"
logstash_src_conf_path: "/home/administrateur/playbooks/elk/logstash/src/"
logstash_dst_conf_path: "/etc/logstash/conf.d/"
logstash_dst_certs_path: "/opt/rsyslog"
logstash_server_private_ip: "192.168.122.26"
logstash_rsyslog_path: "/etc/rsyslog.conf"
logstash_ssl_cfg: "/etc/ssl/openssl.cnf"
```
